---
title: "删除函数 （非托管 API 参考）"
description: "Delete 函数从 CIM 类定义中删除指定的属性和所有其限定符。"
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: reference
api_name:
- Delete
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Delete
helpviewer_keywords:
- Delete function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 30f5bf651990cafe06811019cf2b3d92f866f646
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="delete-function"></a>删除函数
从 CIM 类定义中删除指定的属性和所有其限定符。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>语法  
  
```  
HRESULT Delete (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LPCWSTR           wszName 
); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]未使用此参数。

`ptr`  
[in]指向的指针[IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx)实例。

`wszName`  
[in]要删除的属性名称。 `wszName`必须为有效的指针`LPCWSTR`。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，或者你可以定义它们常量作为在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | 无法删除属性。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszzName` 无效。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 指定的属性不存在。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存来完成该操作。 |
| `WBEM_E_PROPAGATED_PROPERTY` | 0x8004101c | 从基类继承属性。 |
| `WBEM_E_SYSTEM_PROPERTY` | | 属性是系统属性。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
| `WBEM_E_RESET_TO_DEFAULT` | 0x80041030 | 删除当前类的替代默认值的函数。 父类中此属性的默认值已被 reactiviated。 | 

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::Delete](https://msdn.microsoft.com/library/aa391438(v=vs.85).aspx)方法。

## <a name="requirements"></a>惠?  
 **平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅  
[WMI 和性能计数器 （非托管 API 参考）](index.md)
