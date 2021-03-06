---
title: "%= 运算符（C# 参考）"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: '%=_CSharpKeyword'
helpviewer_keywords:
- modulus assignment operator (=%) [C#]
- '%= assignment operator (modulus assignment) [C#]'
ms.assetid: 47e5f068-1d97-4010-bd3b-e21b5d3a77f5
caps.latest.revision: "20"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9bafd0078153e29fbf923948d9b380d4795c3d35
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="-operator-c-reference"></a>%= 运算符（C# 参考）
余数赋值运算符。  
  
## <a name="remarks"></a>备注  
 使用 `%=` 赋值运算符的表达式，如  
  
```  
x %= y  
```  
  
 等效于  
  
```  
x = x % y  
```  
  
 不同的是 `x` 只计算一次。 针对数值类型预定义了 [% 运算符](../../../csharp/language-reference/operators/modulus-operator.md)以计算除法的余数。  
  
 不能直接重载 `%=` 运算符，但用户定义的类型可重载 [% 运算符](../../../csharp/language-reference/operators/modulus-operator.md)（请参阅[运算符（C# 参考）](../../../csharp/language-reference/keywords/operator.md)）。  
  
## <a name="example"></a>示例  
 [!code-csharp[csRefOperators#4](../../../csharp/language-reference/operators/codesnippet/CSharp/modulus-assignment-operator_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [C# 运算符](../../../csharp/language-reference/operators/index.md)
