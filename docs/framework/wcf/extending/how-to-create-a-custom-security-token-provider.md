---
title: "如何：创建自定义安全令牌提供程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], providing credentials
ms.assetid: db8cb478-aa43-478b-bf97-c6489ad7c7fd
caps.latest.revision: 
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload:
- dotnet
ms.openlocfilehash: 37e7f9541457c475bfe187485520df63a84f7555
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-create-a-custom-security-token-provider"></a>如何：创建自定义安全令牌提供程序
本主题介绍如何使用自定义安全令牌提供程序来创建新令牌类型，以及如何将该提供程序与自定义安全令牌管理器集成。  
  
> [!NOTE]
>  如果在 <xref:System.IdentityModel.Tokens> 命名空间中找到的系统提供的令牌不符合要求，请创建一个自定义令牌提供程序。  
  
 安全令牌提供程序会基于客户端或服务凭据中的信息创建一个安全令牌表示形式。 若要在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 安全中使用自定义安全令牌提供程序，则必须创建自定义凭据和安全令牌管理器实现。  
  
 有关自定义凭据和安全令牌管理器的详细信息请参阅[演练： 创建自定义客户端和服务凭据](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)。  
  
 安全令牌的经理、 提供程序和身份验证器类，有关凭据的详细信息，请参阅[安全体系结构](http://msdn.microsoft.com/library/16593476-d36a-408d-808c-ae6fd483e28f)。  
  
### <a name="to-create-a-custom-security-token-provider"></a>创建自定义安全令牌提供程序  
  
1.  定义一个从 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 类派生的新类。  
  
2.  实现 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 方法。 该方法负责创建和返回安全令牌的实例。 下面的示例创建一个名为 `MySecurityTokenProvider` 的类，并重写 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 方法以返回 <xref:System.IdentityModel.Tokens.X509SecurityToken> 类的实例。 该类构造函数需要 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 类的一个实例。  
  
     [!code-csharp[c_CustomTokenProvider#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#1)]
     [!code-vb[c_CustomTokenProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#1)]  
  
### <a name="to-integrate-a-custom-security-token-provider-with-a-custom-security-token-manager"></a>将自定义安全令牌提供程序与自定义安全令牌管理器集成  
  
1.  定义一个从 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 类派生的新类。 （下面的示例从 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 类派生，而该类又从 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 类派生。）  
  
2.  重写 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 方法（如果尚未重写它）。  
  
     <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 方法负责返回 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 类的一个实例，该实例与通过 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 安全框架传递给该方法的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 参数相对应。 修改此方法，以便在用相应的安全令牌参数调用它时，可以返回所实现的自定义安全令牌提供程序（在上一个过程中创建的）。 有关安全令牌管理器的详细信息，请参阅[演练： 创建自定义客户端和服务凭据](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)。  
  
3.  向该方法中添加自定义逻辑，使其可以基于 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 参数返回自定义安全令牌提供程序。 下面的示例在满足令牌要求时返回自定义安全令牌提供程序。 这些要求包括一个 X.509 安全令牌以及消息方向（使用令牌进行消息输出）。 对于其他所有情况，该代码通过调用基类，针对其他安全令牌需求来维护系统提供的行为。  
  
 [!code-csharp[c_CustomTokenProvider#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#2)]
 [!code-vb[c_CustomTokenProvider#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#2)]  
  
## <a name="example"></a>示例  
 下面演示了一个完整的 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 实现，连同相应的 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 实现。  
  
 [!code-csharp[c_CustomTokenProvider#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#0)]
 [!code-vb[c_CustomTokenProvider#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#0)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.IdentityModel.Selectors.SecurityTokenProvider>  
 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>  
 <xref:System.IdentityModel.Selectors.SecurityTokenManager>  
 <xref:System.IdentityModel.Tokens.X509SecurityToken>  
 [演练：创建自定义客户端和服务凭据](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)  
 [如何：创建自定义安全令牌验证器](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)  
 [安全体系结构](http://msdn.microsoft.com/library/16593476-d36a-408d-808c-ae6fd483e28f)
