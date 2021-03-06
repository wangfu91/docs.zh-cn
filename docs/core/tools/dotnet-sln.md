---
title: dotnet sln 命令
description: 使用 dotnet-sln 命令，可以便捷地在解决方案文件中添加、删除和列出项目。
ms.date: 02/14/2020
ms.openlocfilehash: efe52f64a29c8825070bae9ee96b430b32176ffa
ms.sourcegitcommit: 2560a355c76b0a04cba0d34da870df9ad94ceca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89053026"
---
# <a name="dotnet-sln"></a>dotnet sln

**本文适用于：** ✔️ .NET Core 2.x SDK 及更高版本

## <a name="name"></a>“属性”

`dotnet sln` - 在 .NET Core 解决方案文件中列出或修改项目。

## <a name="synopsis"></a>摘要

```dotnetcli
dotnet sln [<SOLUTION_FILE>] [command]

dotnet sln [command] -h|--help
```

## <a name="description"></a>描述

使用 `dotnet sln` 命令，可以便捷地在解决方案文件中列出和修改项目。

若要使用 `dotnet sln` 命令，必须存在解决方案文件。 如果需要创建一个解决方案文件，请使用 [dotnet new](dotnet-new.md) 命令，如下例所示：

```dotnetcli
dotnet new sln
```

## <a name="arguments"></a>自变量

- **`SOLUTION_FILE`**

  要使用的解决方案文件。 如果省略此参数，此命令会搜索当前目录来获取一个解决方案文件。 如果未找到解决方案文件或找到多个解决方案文件，则该命令将失败。

## <a name="options"></a>选项

- **`-h|--help`**

  打印出有关如何使用命令的说明。

## <a name="commands"></a>命令

### `list`

列出解决方案文件中的所有项目。

#### <a name="synopsis"></a>摘要

```dotnetcli
dotnet sln list [-h|--help]
```

#### <a name="arguments"></a>自变量

- **`SOLUTION_FILE`**

  要使用的解决方案文件。 如果省略此参数，此命令会搜索当前目录来获取一个解决方案文件。 如果未找到解决方案文件或找到多个解决方案文件，则该命令将失败。

#### <a name="options"></a>选项

- **`-h|--help`**

  打印出有关如何使用命令的说明。
  
### `add`

将一个或多个项目添加到解决方案文件。

#### <a name="synopsis"></a>摘要

```dotnetcli
dotnet sln [<SOLUTION_FILE>] add [--in-root] [-s|--solution-folder <PATH>] <PROJECT_PATH> [<PROJECT_PATH>...]
dotnet sln add [-h|--help]
```

#### <a name="arguments"></a>自变量

- **`SOLUTION_FILE`**

  要使用的解决方案文件。 如果未指定，此命令会搜索当前目录以获取一个解决方案文件，如果找到多个解决方案文件，则该命令将失败。

- **`PROJECT_PATH`**

  要添加到解决方案的一个或多个项目的路径。 Unix/Linux shell [glob 模式](https://en.wikipedia.org/wiki/Glob_(programming))扩展由 `dotnet sln` 命令正确处理。

#### <a name="options"></a>选项

- **`-h|--help`**

  打印出有关如何使用命令的说明。

- **`--in-root`**

  将项目放在解决方案的根目录下，而不是创建解决方案文件夹。 自 .NET Core 3.0 SDK 起可用。

- **`-s|--solution-folder <PATH>`**

  要将项目添加到的目标解决方案文件夹路径。 自 .NET Core 3.0 SDK 起可用。

### `remove`

从解决方案文件中删除一个或多个项目。

#### <a name="synopsis"></a>摘要

```dotnetcli
dotnet sln [<SOLUTION_FILE>] remove <PROJECT_PATH> [<PROJECT_PATH>...]
dotnet sln [<SOLUTION_FILE>] remove [-h|--help]
```

#### <a name="arguments"></a>自变量

- **`SOLUTION_FILE`**

  要使用的解决方案文件。 如果保留未指定，此命令会搜索当前目录以获取一个解决方案文件，如果找到多个解决方案文件，则该命令将失败。

- **`PROJECT_PATH`**

  要添加到解决方案的一个或多个项目的路径。 Unix/Linux shell [glob 模式](https://en.wikipedia.org/wiki/Glob_(programming))扩展由 `dotnet sln` 命令正确处理。

#### <a name="options"></a>选项

- **`-h|--help`**

  打印出有关如何使用命令的说明。

## <a name="examples"></a>示例

- 在解决方案中列出项目：

  ```dotnetcli
  dotnet sln todo.sln list
  ```

- 将一个 C# 项目添加到解决方案中：

  ```dotnetcli
  dotnet sln add todo-app/todo-app.csproj
  ```

- 从解决方案中删除一个 C# 项目：

  ```dotnetcli
  dotnet sln remove todo-app/todo-app.csproj
  ```

- 将多个 C# 项目添加到解决方案的根目录中：

  ```dotnetcli
  dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj --in-root
  ```

- 将多个 C# 项目添加到解决方案中：

  ```dotnetcli
  dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj
  ```

- 从解决方案中删除多个 C# 项目：

  ```dotnetcli
  dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj
  ```

- 使用 glob 模式（仅限 Unix/Linux）将多个 C# 项目添加到解决方案中：

  ```dotnetcli
  dotnet sln todo.sln add **/*.csproj
  ```

- 使用 globbing 模式（仅限 Windows PowerShell）将多个 C# 项目添加到解决方案中：

  ```dotnetcli
  dotnet sln todo.sln add (ls -r **/*.csproj)
  ```

- 使用 glob 模式（仅限 Unix/Linux）将多个 C# 项目从解决方案中删除：

  ```dotnetcli
  dotnet sln todo.sln remove **/*.csproj
  ```

- 使用 globbing 模式（仅限 Windows PowerShell）将多个 C# 项目从解决方案中删除：

  ```dotnetcli
  dotnet sln todo.sln remove (ls -r **/*.csproj)
  ```
