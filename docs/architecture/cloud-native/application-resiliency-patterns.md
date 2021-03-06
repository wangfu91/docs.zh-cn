---
title: 应用程序复原能力模式
description: 构建适用于 Azure 的云本机 .NET 应用 |应用程序复原模式
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: e81d6e1d6b95cf0053de3ba557068ff458a59dc9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91161147"
---
# <a name="application-resiliency-patterns"></a>应用程序复原能力模式

第一道防线是应用程序复原能力。

虽然您可以投入大量时间来编写自己的复原框架，此类产品已经存在。 [Polly](http://www.thepollyproject.org/) 是一个全面的 .net 复原和暂时性故障处理库，使开发人员能够以流畅且线程安全的方式表达复原策略。 Polly 以 .NET Framework 或 .NET Core 生成的目标应用程序为目标。 下表介绍了 Polly 库中提供的复原功能（称为 `policies` ）。 它们可单独应用或组合在一起。

| 策略 | 体验 |
| :-------- | :-------- |
| 重试 | 配置针对指定操作的重试操作。 |
| 断路器 | 当故障超过配置的阈值时，阻止预定义时间段内请求的操作 |
| 超时 | 对调用方可以等待响应的持续时间的限制。 |
| 隔舱 | 将操作限制为固定大小的资源池，以防止从对资源 swamping 的调用失败。 |
| 缓存 | 自动存储响应。 |
| 回退 | 定义发生故障时的结构化行为。 |

请注意上图中的如何将复原策略应用于请求消息，无论是来自外部客户端还是后端服务。 目标是对可能暂时不可用的服务的请求进行补偿。 通常，这些生存期较短的中断会自行列出，其中包含下表中所示的 HTTP 状态代码。

| HTTP 状态代码| 原因 |
| :-------- | :-------- |
| 404 | 未找到 |
| 408 | 请求超时 |
| 429 | 请求过多 (你很可能已受到限制)  |
| 502 | 网关错误 |
| 503 | 服务不可用 |
| 504 | 网关超时 |

问：是否要重试 HTTP 状态代码 403-禁止访问？ 不是。 此时，系统将正常运行，但通知调用方他们无权执行所请求的操作。 必须注意仅重试由失败导致的操作。

如第1章所述，Microsoft 开发云本机应用程序的开发人员应以 .NET Core 平台为目标。 版本2.1 引入了 [HTTPClientFactory](https://www.stevejgordon.co.uk/introduction-to-httpclientfactory-aspnetcore) 库，用于创建用于与基于 URL 的资源交互的 HTTP 客户端实例。 工厂类取代了原始 HTTPClient 类，它支持许多增强功能，其中一个功能与 Polly 复原库 [紧密集成](../microservices/implement-resilient-applications/implement-http-call-retries-exponential-backoff-polly.md) 。 利用它，你可以轻松地在应用程序启动类中定义复原策略来处理部分故障和连接问题。

接下来，让我们展开重试和断路器模式。

### <a name="retry-pattern"></a>重试模式

在分布式云本机环境中，对服务和云资源的调用可能会失败，这是由于暂时性 (短暂的) 故障，通常在短暂的一段时间内自行更正。 实现重试策略可帮助云本机服务降低这些方案。

使用 [重试模式](/azure/architecture/patterns/retry) ，服务可以重试失败的请求操作， (可配置的) 次，且等待时间呈指数级增长。 图6-2 显示了一个重试操作。

![操作中的重试模式](./media/retry-pattern.png)

**图 6-2**。 操作中的重试模式

在上图中，已为请求操作实现重试模式。 它配置为允许最多四次重试，而不能使用回退时间间隔 (等待时间，) 从两秒开始，每次后续尝试都呈指数级增长。

- 第一次调用失败并返回 HTTP 状态代码500。 应用程序等待两秒钟，然后重试呼叫。
- 第二次调用也失败，并返回 HTTP 状态代码500。 现在，应用程序将回退间隔加倍到4秒，然后重试该调用。
- 最后，第三次调用成功。
- 在此方案中，重试操作最多尝试四次重试，同时在调用失败之前将回退持续时间加倍。
- 如果第四次重试失败，则将调用回退策略来正常处理此问题。

在重试调用以允许服务时间自动更正之前，请务必增加回退时间。 最佳做法是，在每次重试) 时，将以指数方式增加的回退 (翻倍，以允许适当的更正时间。

## <a name="circuit-breaker-pattern"></a>断路器模式

尽管重试模式可以在部分失败时帮助抢救请求放大，但在某些情况下，可能会由于意外的事件需要更长的时间来解决，导致失败。 这些故障轻则导致部分连接中断，重则导致服务完全瘫痪。 在这些情况下，应用程序不必再重试不太可能成功的操作。

要使问题更糟，对非响应式服务执行连续重试操作可以让你进入一个自行施加的拒绝服务方案，在这种情况下，你的服务将持续调用耗尽资源（如内存、线程和数据库连接），从而导致系统上使用相同资源的无关部分出现故障。

在这种情况下，操作会立即失败并仅在有可能成功的情况下尝试调用服务，这是最好的做法。

[断路器模式](/azure/architecture/patterns/circuit-breaker)可以防止应用程序重复尝试执行很可能失败的操作。 在预定义的失败调用数后，它会阻止到服务的所有流量。 它会定期调用，以确定是否已解决错误。 图6-3 显示了操作中的断路器模式。

![操作中的断路器模式](./media/circuit-breaker-pattern.png)

**图 6-3**。 操作中的断路器模式

在上图中，已将断路器模式添加到原始重试模式。 请注意，100请求失败后，电路熔断器会打开，不再允许对服务进行调用。 CheckCircuit 值设置为30秒，指定库允许一个请求继续到服务的频率。 如果该调用成功，线路将关闭，并且服务再次可用于通信。

请记住，断路器模式的目的 *不同* 于重试模式。 重试模式使应用程序能够在预期成功的情况下重试操作。 断路器模式可以防止应用程序执行可能会失败的操作。 通常情况下，应用程序将使用重试模式通过断路器调用操作来 *合并* 这两种模式。

## <a name="testing-for-resiliency"></a>测试复原能力

针对复原的测试始终无法通过运行单元测试、集成测试等)  (测试应用程序功能。 必须在故障状态下测试端到端工作负荷的执行情况，而这种状态只能间歇性地出现。 例如：通过使进程崩溃、过期证书，使从属服务不可用等来注入故障。混乱的框架（如 [混乱）](https://github.com/Netflix/chaosmonkey) 可用于这样的混乱测试。

应用程序复原能力是处理请求的操作时必须执行的操作。 但这只是故事的一半。 接下来，我们介绍 Azure 云中提供的复原功能。

>[!div class="step-by-step"]
>[上一页](resiliency.md)
>[下一页](infrastructure-resiliency-azure.md)
