---
title: 应用互操作特性
ms.date: 03/30/2017
helpviewer_keywords:
- design-time attributes
- .NET Framework, exposing components to COM
- attributes [.NET Framework], design-time functionality
- conversion-tool attributes
- attributes [.NET Framework], interop-specific
- attributes [.NET Framework], conversion-tool
- interoperation with unmanaged code, applying attributes
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
- COM interop, applying attributes
ms.assetid: b6014613-641c-4912-9e2f-83a99210a037
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 27d1a8cc80db9e17000880c006ac1d7c1bd12fec
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631491"
---
# <a name="applying-interop-attributes"></a><span data-ttu-id="1dff9-102">应用互操作特性</span><span class="sxs-lookup"><span data-stu-id="1dff9-102">Applying Interop Attributes</span></span>
<span data-ttu-id="1dff9-103"><xref:System.Runtime.InteropServices> 命名空间提供三类特定于互操作的特性：在设计时由你应用的特性、在转换进程中由 COM 互操作工具和 API 应用的特性以及由你或 COM 互操作应用的特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-103">The <xref:System.Runtime.InteropServices> namespace provides three categories of interop-specific attributes: those applied by you at design time, those applied by COM interop tools and APIs during the conversion process, and those applied either by you or COM interop.</span></span>  
  
 <span data-ttu-id="1dff9-104">如果不熟悉将特性应用到托管代码的任务，请参阅[利用特性扩展元数据](../../../docs/standard/attributes/index.md)。</span><span class="sxs-lookup"><span data-stu-id="1dff9-104">If you are unfamiliar with the task of applying attributes to managed code, see [Extending Metadata Using Attributes](../../../docs/standard/attributes/index.md).</span></span> <span data-ttu-id="1dff9-105">如其他自定义特性一样，可以将特定于互操作的特性应用于类型、方法、属性、参数、字段和其他成员。</span><span class="sxs-lookup"><span data-stu-id="1dff9-105">Like other custom attributes, you can apply interop-specific attributes to types, methods, properties, parameters, fields, and other members.</span></span>  
  
## <a name="design-time-attributes"></a><span data-ttu-id="1dff9-106">设计时特性</span><span class="sxs-lookup"><span data-stu-id="1dff9-106">Design-Time Attributes</span></span>  
 <span data-ttu-id="1dff9-107">可以使用设计时特性调整由 COM 互操作工具和 API 执行的转换进程的结果。</span><span class="sxs-lookup"><span data-stu-id="1dff9-107">You can adjust the outcome of the conversion process performed by COM interop tools and APIs by using design-time attributes.</span></span> <span data-ttu-id="1dff9-108">下表介绍了可以应用到托管源代码的特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-108">The following table describes the attributes that you can apply to your managed source code.</span></span> <span data-ttu-id="1dff9-109">有时，COM 互操作工具也可能应用此表中所述的特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-109">COM interop tools, on occasion, might also apply the attributes described in this table.</span></span>  
  
|<span data-ttu-id="1dff9-110">属性</span><span class="sxs-lookup"><span data-stu-id="1dff9-110">Attribute</span></span>|<span data-ttu-id="1dff9-111">说明</span><span class="sxs-lookup"><span data-stu-id="1dff9-111">Description</span></span>|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.AutomationProxyAttribute>|<span data-ttu-id="1dff9-112">指定应使用自动化封送处理程序还是自定义代理和存根对类型进行封送处理。</span><span class="sxs-lookup"><span data-stu-id="1dff9-112">Specifies whether the type should be marshaled using the Automation marshaler or a custom proxy and stub.</span></span>|  
|<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>|<span data-ttu-id="1dff9-113">控制为类生成的接口类型。</span><span class="sxs-lookup"><span data-stu-id="1dff9-113">Controls the type of interface generated for a class.</span></span>|  
|<xref:System.Runtime.InteropServices.CoClassAttribute>|<span data-ttu-id="1dff9-114">标识从类型库导入的原始组件类的 CLSID。</span><span class="sxs-lookup"><span data-stu-id="1dff9-114">Identifies the CLSID of the original coclass imported from a type library.</span></span><br /><br /> <span data-ttu-id="1dff9-115">COM 互操作工具通常应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-115">COM interop tools typically apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.ComImportAttribute>|<span data-ttu-id="1dff9-116">指示组件类或接口定义是从 COM 类型库导入的。</span><span class="sxs-lookup"><span data-stu-id="1dff9-116">Indicates that a coclass or interface definition was imported from a COM type library.</span></span> <span data-ttu-id="1dff9-117">运行时使用此标记来确定如何对类型进行激活和封送处理。</span><span class="sxs-lookup"><span data-stu-id="1dff9-117">The runtime uses this flag to know how to activate and marshal the type.</span></span> <span data-ttu-id="1dff9-118">此特性禁止将类型导入回类型库。</span><span class="sxs-lookup"><span data-stu-id="1dff9-118">This attribute prohibits the type from being exported back to a type library.</span></span><br /><br /> <span data-ttu-id="1dff9-119">COM 互操作工具通常应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-119">COM interop tools typically apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>|<span data-ttu-id="1dff9-120">指定在从 COM 注册程序集以使用时应调用的方法，这样在注册过程中可以执行用户编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1dff9-120">Indicates that a method should be called when the assembly is registered for use from COM, so that user-written code can be executed during the registration process.</span></span>|  
|<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>|<span data-ttu-id="1dff9-121">标识类的事件源的接口。</span><span class="sxs-lookup"><span data-stu-id="1dff9-121">Identifies interfaces that are sources of events for the class.</span></span><br /><br /> <span data-ttu-id="1dff9-122">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-122">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>|<span data-ttu-id="1dff9-123">指示在从 COM 取消注册程序集时应调用的方法，这样用户编写的代码可以在过程中执行。</span><span class="sxs-lookup"><span data-stu-id="1dff9-123">Indicates that a method should be called when the assembly is unregistered from COM, so that user-written code can execute during the process.</span></span>|  
|<xref:System.Runtime.InteropServices.ComVisibleAttribute>|<span data-ttu-id="1dff9-124">当特性值为“false”时，将使类型对 COM 不可见  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-124">Renders types invisible to COM when the attribute value equals **false**.</span></span> <span data-ttu-id="1dff9-125">此特性可以应用于单个类型或整个程序集，以控制 COM 的可见性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-125">This attribute can be applied to an individual type or to an entire assembly to control COM visibility.</span></span> <span data-ttu-id="1dff9-126">默认情况下，所有托管的公共类型都是可见的；不需要使用此特性来使它们可见。</span><span class="sxs-lookup"><span data-stu-id="1dff9-126">By default, all managed, public types are visible; the attribute is not needed to make them visible.</span></span>|  
|<xref:System.Runtime.InteropServices.DispIdAttribute>|<span data-ttu-id="1dff9-127">指定方法或字段的 COM 调度标识符 (DISPID)。</span><span class="sxs-lookup"><span data-stu-id="1dff9-127">Specifies the COM dispatch identifier (DISPID) of a method or field.</span></span> <span data-ttu-id="1dff9-128">此特性包含适用于它所述的方法、字段或属性的 DISPID。</span><span class="sxs-lookup"><span data-stu-id="1dff9-128">This attribute contains the DISPID for the method, field, or property it describes.</span></span><br /><br /> <span data-ttu-id="1dff9-129">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-129">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.FieldOffsetAttribute>|<span data-ttu-id="1dff9-130">指示当用于 StructLayoutAttribute 时类中每个字段的物理位置，并且将 LayoutKind 设置为 Explicit   。</span><span class="sxs-lookup"><span data-stu-id="1dff9-130">Indicates the physical position of each field within a class when used with the **StructLayoutAttribute**, and the **LayoutKind** is set to Explicit.</span></span>|  
|<xref:System.Runtime.InteropServices.GuidAttribute>|<span data-ttu-id="1dff9-131">指定类、接口或整个类型库的全局唯一标识符 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="1dff9-131">Specifies the globally unique identifier (GUID) of a class, interface, or an entire type library.</span></span> <span data-ttu-id="1dff9-132">传递到此特性的字符串必须是 System.Guid 类型可接受的构造函数参数的格式  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-132">The string passed to the attribute must be a format that is an acceptable constructor argument for the type **System.Guid**.</span></span><br /><br /> <span data-ttu-id="1dff9-133">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-133">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.IDispatchImplAttribute>|<span data-ttu-id="1dff9-134">指示当向 COM 公开双重接口和调度时，公共语言运行时使用哪个 IDispatch 接口实现  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-134">Indicates which **IDispatch** interface implementation the common language runtime uses when exposing dual interfaces and dispinterfaces to COM.</span></span>|  
|<xref:System.Runtime.InteropServices.InAttribute>|<span data-ttu-id="1dff9-135">指示数据应封送到调用方。</span><span class="sxs-lookup"><span data-stu-id="1dff9-135">Indicates that data should be marshaled in to the caller.</span></span> <span data-ttu-id="1dff9-136">可用于特性参数。</span><span class="sxs-lookup"><span data-stu-id="1dff9-136">Can be used to attribute parameters.</span></span>|  
|<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>|<span data-ttu-id="1dff9-137">控制如何向 COM 客户端公开托管接口（仅限于双重、IUnknown-derived 或 IDispatch）。</span><span class="sxs-lookup"><span data-stu-id="1dff9-137">Controls how a managed interface is exposed to COM clients (Dual, IUnknown-derived, or IDispatch only).</span></span><br /><br /> <span data-ttu-id="1dff9-138">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-138">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.LCIDConversionAttribute>|<span data-ttu-id="1dff9-139">指示非托管的方法签名应具有 LCID 参数。</span><span class="sxs-lookup"><span data-stu-id="1dff9-139">Indicates that an unmanaged method signature expects an LCID parameter.</span></span><br /><br /> <span data-ttu-id="1dff9-140">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-140">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.MarshalAsAttribute>|<span data-ttu-id="1dff9-141">指示应如何在托管和非托管代码之间封送处理字段或参数中的数据。</span><span class="sxs-lookup"><span data-stu-id="1dff9-141">Indicates how the data in fields or parameters should be marshaled between managed and unmanaged code.</span></span> <span data-ttu-id="1dff9-142">此特性始终是可选的，因为每个数据类型都具有默认的封送处理行为。</span><span class="sxs-lookup"><span data-stu-id="1dff9-142">The attribute is always optional because each data type has default marshaling behavior.</span></span><br /><br /> <span data-ttu-id="1dff9-143">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-143">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.OptionalAttribute>|<span data-ttu-id="1dff9-144">指示参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="1dff9-144">Indicates that a parameter is optional.</span></span><br /><br /> <span data-ttu-id="1dff9-145">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-145">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.OutAttribute>|<span data-ttu-id="1dff9-146">指示字段或参数中的数据必须从调用的对象被封送回其调用方。</span><span class="sxs-lookup"><span data-stu-id="1dff9-146">Indicates that the data in a field or parameter must be marshaled from a called object back to its caller.</span></span>|  
|<xref:System.Runtime.InteropServices.PreserveSigAttribute>|<span data-ttu-id="1dff9-147">取消一般在互操作调用过程中发生的 HRESULT 或 retval 签名转换。</span><span class="sxs-lookup"><span data-stu-id="1dff9-147">Suppresses the HRESULT or retval signature transformation that normally takes place during interoperation calls.</span></span> <span data-ttu-id="1dff9-148">特性会影响封送处理以及类型库导出。</span><span class="sxs-lookup"><span data-stu-id="1dff9-148">The attribute affects marshaling as well as type library exporting.</span></span><br /><br /> <span data-ttu-id="1dff9-149">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-149">COM interop tools can apply this attribute.</span></span>|  
|<xref:System.Runtime.InteropServices.ProgIdAttribute>|<span data-ttu-id="1dff9-150">指定 .NET Framework 类的 ProgID。</span><span class="sxs-lookup"><span data-stu-id="1dff9-150">Specifies the ProgID of a .NET Framework class.</span></span> <span data-ttu-id="1dff9-151">可用于特性类。</span><span class="sxs-lookup"><span data-stu-id="1dff9-151">Can be used to attribute classes.</span></span>|  
|<xref:System.Runtime.InteropServices.StructLayoutAttribute>|<span data-ttu-id="1dff9-152">控制类的字段的物理布局。</span><span class="sxs-lookup"><span data-stu-id="1dff9-152">Controls the physical layout of the fields of a class.</span></span><br /><br /> <span data-ttu-id="1dff9-153">COM 互操作工具可以应用此特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-153">COM interop tools can apply this attribute.</span></span>|  
  
## <a name="conversion-tool-attributes"></a><span data-ttu-id="1dff9-154">转换工具特性</span><span class="sxs-lookup"><span data-stu-id="1dff9-154">Conversion-Tool Attributes</span></span>  
 <span data-ttu-id="1dff9-155">下表介绍了转换过程期间 COM 互操作工具应用的特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-155">The following table describes attributes that COM interop tools apply during the conversion process.</span></span> <span data-ttu-id="1dff9-156">不要在设计时应用这些特性。</span><span class="sxs-lookup"><span data-stu-id="1dff9-156">You do not apply these attributes at design time.</span></span>  
  
|<span data-ttu-id="1dff9-157">属性</span><span class="sxs-lookup"><span data-stu-id="1dff9-157">Attribute</span></span>|<span data-ttu-id="1dff9-158">说明</span><span class="sxs-lookup"><span data-stu-id="1dff9-158">Description</span></span>|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.ComAliasNameAttribute>|<span data-ttu-id="1dff9-159">指示参数或字段类型的 COM 别名。</span><span class="sxs-lookup"><span data-stu-id="1dff9-159">Indicates the COM alias for a parameter or field type.</span></span> <span data-ttu-id="1dff9-160">可用于特性参数、字段或返回值。</span><span class="sxs-lookup"><span data-stu-id="1dff9-160">Can be used to attribute parameters, fields, or return values.</span></span>|  
|<xref:System.Runtime.InteropServices.ComConversionLossAttribute>|<span data-ttu-id="1dff9-161">指示有关类或接口的信息从类型库被导入到程序集时丢失。</span><span class="sxs-lookup"><span data-stu-id="1dff9-161">Indicates that information about a class or interface was lost when it was imported from a type library to an assembly.</span></span>|  
|<xref:System.Runtime.InteropServices.ComEventInterfaceAttribute>|<span data-ttu-id="1dff9-162">标识源接口和实现事件接口的方法的类。</span><span class="sxs-lookup"><span data-stu-id="1dff9-162">Identifies the source interface and the class that implements the methods of the event interface.</span></span>|  
|<xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute>|<span data-ttu-id="1dff9-163">指示程序集最初是从 COM 类型库导入的。</span><span class="sxs-lookup"><span data-stu-id="1dff9-163">Indicates that the assembly was originally imported from a COM type library.</span></span> <span data-ttu-id="1dff9-164">此特性包含原始类型库的类型库定义。</span><span class="sxs-lookup"><span data-stu-id="1dff9-164">This attribute contains the type library definition of the original type library.</span></span>|  
|<xref:System.Runtime.InteropServices.TypeLibFuncAttribute>|<span data-ttu-id="1dff9-165">包含最初从 COM 类型库为此功能导入的 FUNCFLAGS  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-165">Contains the **FUNCFLAGS** that were originally imported for this function from the COM type library.</span></span>|  
|<xref:System.Runtime.InteropServices.TypeLibTypeAttribute>|<span data-ttu-id="1dff9-166">包含最初从 COM 类型库为此类型导入的 TYPEFLAGS  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-166">Contains the **TYPEFLAGS** that were originally imported for this type from the COM type library.</span></span>|  
|<xref:System.Runtime.InteropServices.TypeLibVarAttribute>|<span data-ttu-id="1dff9-167">包含最初从 COM 类型库为此变量导入的 VARFLAGS  。</span><span class="sxs-lookup"><span data-stu-id="1dff9-167">Contains the **VARFLAGS** that were originally imported for this variable from the COM type library.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="1dff9-168">请参阅</span><span class="sxs-lookup"><span data-stu-id="1dff9-168">See also</span></span>

- <xref:System.Runtime.InteropServices>
- [<span data-ttu-id="1dff9-169">向 COM 公开 .NET Framework 组件</span><span class="sxs-lookup"><span data-stu-id="1dff9-169">Exposing .NET Framework Components to COM</span></span>](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)
- [<span data-ttu-id="1dff9-170">属性</span><span class="sxs-lookup"><span data-stu-id="1dff9-170">Attributes</span></span>](../../../docs/standard/attributes/index.md)
- [<span data-ttu-id="1dff9-171">为互操作限定 .NET 类型</span><span class="sxs-lookup"><span data-stu-id="1dff9-171">Qualifying .NET Types for Interoperation</span></span>](../../../docs/standard/native-interop/qualify-net-types-for-interoperation.md)
- [<span data-ttu-id="1dff9-172">打包用于 COM 的 .NET Framework 程序集</span><span class="sxs-lookup"><span data-stu-id="1dff9-172">Packaging a .NET Framework Assembly for COM</span></span>](../../../docs/framework/interop/packaging-an-assembly-for-com.md)