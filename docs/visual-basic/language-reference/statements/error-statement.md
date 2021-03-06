---
title: "Error 语句"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords: vb.error
helpviewer_keywords:
- Error statement [Visual Basic], syntax
- Error statement [Visual Basic]
- Error keyword [Visual Basic]
- run-time errors [Visual Basic], codes
- errors [Visual Basic], simulating
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 3cd3245fd3e9e62b1b6443e9787c97808a0d179d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="error-statement"></a>Error 语句
模拟出错的匹配项。  
  
## <a name="syntax"></a>语法  
  
```  
Error errornumber  
```  
  
## <a name="parts"></a>部件  
 `errornumber`  
 必需。 可以是任何有效的错误号。  
  
## <a name="remarks"></a>备注  
 `Error`向后兼容性支持语句。 在新代码，尤其是在创建对象时，使用`Err`对象的`Raise`方法以生成运行时错误。  
  
 如果`errornumber`定义，`Error`语句后的属性调用错误处理程序`Err`对象分配以下默认值：  
  
|属性|值|  
|--------------|-----------|  
|`Number`|指定为参数的值`Error`语句。 可以是任何有效的错误号。|  
|`Source`|当前的 Visual Basic 项目的名称。|  
|`Description`|字符串对应的返回值的表达式`Error`函数为指定`Number`，如果存在此字符串。 如果字符串不存在，`Description`包含零长度字符串 ("")。|  
|`HelpFile`|完全限定的驱动器、 路径和相应的 Visual Basic 帮助文件的文件名。|  
|`HelpContext`|相应的 Visual Basic 帮助文件对应的错误的上下文 ID`Number`属性。|  
|`LastDLLError`|为零。|  
  
 如果没有错误处理程序存在，或者如果未启用，创建并从显示一条错误消息`Err`对象属性。  
  
> [!NOTE]
>  某些 Visual Basic 主机应用程序无法创建对象。 请参阅主机应用程序的文档，以确定它是否可以创建类和对象。  
  
## <a name="example"></a>示例  
 此示例使用`Error`语句生成错误号 11。  
  
```  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## <a name="requirements"></a>要求  
 **Namespace:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **程序集：** Visual Basic 运行库 （在 Microsoft.VisualBasic.dll 中)  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>  
 <xref:Microsoft.VisualBasic.Information.Err%2A>  
 <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>  
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)  
 [Resume 语句](../../../visual-basic/language-reference/statements/resume-statement.md)  
 [错误消息](../../../visual-basic/language-reference/error-messages/index.md)
