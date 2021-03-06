---
title: "标准终结点的用法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ecd6a62f-9619-4778-a497-6f888087a9ea
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0ac8a9c639099e952f6030f5625958dd2bf84757
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="usage-of-standard-endpoints"></a>标准终结点的用法
此示例演示如何在服务配置文件中使用标准终结点。 通过标准终结点，用户可以使用单个属性来描述地址、绑定和协定组合以及与其关联的附加属性，从而简化终结点定义。 此示例演示如何定义和实现自定义标准终结点，以及如何在终结点中定义特定属性。  
  
## <a name="sample-details"></a>示例详细信息  
 可以通过指定地址、绑定和协定这三个参数来指定服务终结点。 可以提供的其他参数包括行为配置、标头、侦听 URI 等。 在某些情况下，任何或所有地址、绑定和协定具有无法更改的值。 因此，可以使用标准终结点。 这类终结点包括元数据交换终结点和发现终结点。 标准终结点还允许配置服务终结点，而不必提供固定性质的信息或创建其自己的标准终结点，从而提高了可用性，例如通过提供一组合理的默认值，从而降低配置文件的详细级别，来提高可用性。  
  
 此示例由两个项目组成：定义两个标准终结点的服务以及与该服务通信的客户端。 下面的示例演示如何为配置文件中的服务定义标准终结点。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <endpointExtensions>  
        <add name="customEndpoint" type="Microsoft.Samples.StandardEndpoints.CustomEndpointCollectionElement, service" />  
      </endpointExtensions>  
    </extensions>  
    <services>  
      <service name="Microsoft.Samples.StandardEndpoints.CalculatorService">  
        <endpoint address="http://localhost:8000/Samples/Service.svc/customEndpoint" contract="Microsoft.Samples.StandardEndpoints.ICalculator" kind="customEndpoint" />  
        <endpoint kind="mexEndpoint" />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <standardEndpoints>  
      <customEndpoint>  
        <standardEndpoint property="True" />  
      </customEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
</configuration>  
```  
  
 为服务定义的第一个终结点的类型为 `customEndpoint`，其定义在 `<standardEndpoints>` 节中，其中为属性 `property` 提供了值 `true`。 这是使用新属性自定义终结点的情况。 第二个终结点对应于元数据终结点，其中地址、绑定和协定的值是固定的。  
  
 若要定义标准终结点元素，必须创建从 `StandardEndpointElement` 派生的类。 在此示例中，已定义了 `CustomEndpointElement` 类，如下面的示例所示。  
  
```csharp  
public class CustomEndpointElement : StandardEndpointElement  
{  
    public bool Property  
    {  
        get { return (bool)base["property"]; }  
        set { base["property"] = value; }  
    }  
  
    protected override ConfigurationPropertyCollection Properties  
    {  
        get  
        {  
            ConfigurationPropertyCollection properties = base.Properties;  
            properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));  
            return properties;  
        }  
    }  
  
    protected override Type EndpointType  
    {  
        get { return typeof(CustomEndpoint); }  
    }  
  
    protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)  
    {  
        return new CustomEndpoint();  
    }  
  
    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)  
    {  
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
        customEndpoint.Property = this.Property;  
    }  
  
    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)  
    {  
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
        customEndpoint.Property = this.Property;  
    }  
  
    protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)  
    {  
    }  
  
    protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)  
    {  
    }  
}  
```  
  
 在 `CreateServiceEndpoint` 函数中，创建了一个 `CustomEndpoint` 对象。 其定义如下面的示例所示。  
  
```  
public class CustomEndpoint : ServiceEndpoint  
    {  
        public CustomEndpoint()  
            : this(string.Empty)  
        {  
        }  
  
        public CustomEndpoint(string address)  
            : this(address, ContractDescription.GetContract(typeof(ICalculator)))  
        {  
        }  
  
        public CustomEndpoint(string address, ContractDescription contract)  
            : base(contract)  
        {  
            this.Binding = new BasicHttpBinding();  
            this.IsSystemEndpoint = false;  
        }  
  
        public bool Property  
        {  
            get;  
            set;  
        }  
    }  
```  
  
 若要在服务与客户端之间执行通信，需要在客户端中创建对服务的服务引用。 当生成和执行示例时，服务会执行，且客户端与之进行通信。 请注意，每次对服务进行更改时，都应更新服务引用。  
  
#### <a name="to-use-this-sample"></a>使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 StandardEndpoints.sln 文件。  
  
2.  使多个项目可以启动。  
  
    1.  在**解决方案资源管理器**，右键单击该标准终结点解决方案，然后选择**属性**。  
  
    2.  在**通用属性**，选择**启动项目**，然后单击**多启动项目**。  
  
    3.  将服务项目移动到列表中，开始使用**操作**设置为**启动**。  
  
    4.  客户端将项目移动服务项目中之后, 还与**操作**设置为**启动**。  
  
         这指定客户端项目在服务项目之后执行。  
  
3.  若要运行解决方案，请按 F5。  
  
> [!NOTE]
>  如果这些步骤不起作用，则通过以下步骤来确保已正确设置环境。  
>   
>  1.  确保已执行[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
> 2.  若要生成解决方案，请按照中的说明[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)。  
> 3.  若要在一个或多个计算机配置上运行示例，请按照中的说明[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问 [针对 .NET Framework 4 的 Windows Communication Foundation (WCF) 和 Windows Workflow Foundation (WF) 示例](http://go.microsoft.com/fwlink/?LinkId=150780) 以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\StandardEndpoints`  
  
## <a name="see-also"></a>请参阅
