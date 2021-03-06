---
title: IHostMalloc 接口
ms.date: 03/30/2017
api_name:
- IHostMAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMAlloc
helpviewer_keywords:
- IHostMAlloc interface [.NET Framework hosting]
ms.assetid: e3c6643b-6fc7-4a99-959d-4b7b4e63fdee
topic_type:
- apiref
ms.openlocfilehash: 8f4e1cd7586df7d8e2a577d26f06eaed6b2c8bb7
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804607"
---
# <a name="ihostmalloc-interface"></a>IHostMalloc 接口
提供允许公共语言运行时（CLR）通过宿主请求从堆进行细化分配的方法。  
  
## <a name="methods"></a>方法  
  
|方法|说明|  
|------------|-----------------|  
|[Alloc 方法](ihostmalloc-alloc-method.md)|请求宿主从堆分配请求的内存量。|  
|[DebugAlloc 方法](ihostmalloc-debugalloc-method.md)|请求宿主从堆分配请求的内存量，并另外跟踪内存的分配位置。|  
|[Free 方法](ihostmalloc-free-method.md)|释放通过使用方法分配的内存 `Alloc` 。|  
  
## <a name="remarks"></a>备注  
 CLR `IHostMalloc` 通过调用[IHostMemoryManager：： CreateMalloc](ihostmemorymanager-createmalloc-method.md)方法获取指向实例的接口指针。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../get-started/system-requirements.md)。  
  
 **标头：** Mscoree.dll  
  
 **库：** 作为资源包括在 Mscoree.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [IHostMemoryManager 接口](ihostmemorymanager-interface.md)
- [承载接口](hosting-interfaces.md)
