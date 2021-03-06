---
title: "如何：更改 Windows 窗体 LinkLabel 控件的外观"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- LinkLabel properties
- LinkLabel control [Windows Forms], changing appearance of links
- links [Windows Forms], changing appearance
- examples [Windows Forms], LinkLabel control
- LinkLabel control [Windows Forms], examples
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7dc3963ab1b242ce8dce53d9bba996f52347679b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-linklabel-control"></a>如何：更改 Windows 窗体 LinkLabel 控件的外观
你可以更改显示的文本<xref:System.Windows.Forms.LinkLabel>控件以满足多种用途。 例如，它是常见的做法，以指示用户后，可以设置要显示在特定颜色带下划线的文本单击文本。 在用户单击文本后的颜色更改为不同的颜色。 若要控制此行为，可以设置五个不同的属性： <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>， <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>， <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>， <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>，和<xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>属性。  
  
### <a name="to-change-the-appearance-of-a-linklabel-control"></a>若要更改 LinkLabel 控件的外观  
  
1.  设置<xref:System.Windows.Forms.LinkLabel.LinkColor%2A>和<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>属性设置为所需的颜色。  
  
     这可以是以编程方式或在设计时在**属性**窗口。  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2.  设置<xref:System.Windows.Forms.LinkLabel.Text%2A>为适当标题的属性。  
  
     这可以是以编程方式或在设计时在**属性**窗口。  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3.  设置<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>属性来确定哪个部分的标题将指示的链接的形式。  
  
     <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>值表示为带有<xref:System.Windows.Forms.LinkArea>包含两个数字、 起始字符位置和字符数。 这可以是以编程方式或在设计时在**属性**窗口。  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4.  设置<xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>属性<xref:System.Windows.Forms.LinkBehavior.AlwaysUnderline>， <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>，或<xref:System.Windows.Forms.LinkBehavior.NeverUnderline>。  
  
     如果设置为<xref:System.Windows.Forms.LinkBehavior.HoverUnderline>，由标题的一部分<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>当指针停留在其上只会带有下划线。  
  
5.  在<xref:System.Windows.Forms.LinkLabel.LinkClicked>事件处理程序中，设置<xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>属性`true`。  
  
     访问链接，很常见的做法通常按颜色更改以某种方式，其外观。 文本将更改为指定的颜色<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>属性。  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>  
 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>  
 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>  
 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>  
 [LinkLabel 控件概述](../../../../docs/framework/winforms/controls/linklabel-control-overview-windows-forms.md)  
 [如何：使用 Windows 窗体 LinkLabel 控件链接到对象或网页](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)  
 [LinkLabel 控件](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)
