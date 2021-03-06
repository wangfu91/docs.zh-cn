---
title: ISymUnmanagedReader2 接口
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2
helpviewer_keywords:
- ISymUnmanagedReader2 interface [.NET Framework debugging]
ms.assetid: a01a881b-82a3-4b3e-a3a9-9dc305c2e5f7
topic_type:
- apiref
ms.openlocfilehash: d4c5ff46d37b1292059b18920abd8042c18bbf31
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615392"
---
# <a name="isymunmanagedreader2-interface"></a>ISymUnmanagedReader2 接口
表示一个符号读取器，该读取器提供对符号存储区中的文档、方法和变量的访问。 此接口扩展[ISymUnmanagedReader](isymunmanagedreader-interface.md)接口。  
  
## <a name="methods"></a>方法  
  
|方法|说明|  
|------------|-----------------|  
|[GetMethodByVersionPreRemap 方法](isymunmanagedreader2-getmethodbyversionpreremap-method.md)|在给定方法标记和编辑并继续版本号的情况下，获取符号读取器方法。|  
|[GetMethodsInDocument 方法](isymunmanagedreader2-getmethodsindocument-method.md)|获取所提供文档中包含行信息的每个方法。|  
|[GetSymAttributePreRemap 方法](isymunmanagedreader2-getsymattributepreremap-method.md)|根据名称获取自定义属性。|  
  
## <a name="requirements"></a>要求  
 **标头：** CorSym，CorSym  
  
## <a name="see-also"></a>另请参阅

- [诊断符号存储区接口](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedReader 接口](isymunmanagedreader-interface.md)
