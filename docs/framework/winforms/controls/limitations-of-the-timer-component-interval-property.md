---
title: Windows 窗体 Timer 组件的限制&#39;s 间隔属性
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- timers [Windows Forms], event intervals
- Interval property [Windows Forms], limitations
- timers [Windows Forms], Windows-based
- Timer component [Windows Forms], limitations of Interval property
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e9c42a0946cf29415f7bb12345da6784e0c276d5
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="limitations-of-the-windows-forms-timer-component39s-interval-property"></a>Windows 窗体 Timer 组件的限制&#39;s 间隔属性
Windows 窗体<xref:System.Windows.Forms.Timer>组件具有<xref:System.Windows.Forms.Timer.Interval%2A>属性，用于指定一个计时器事件和下一步之间传递的毫秒数。 除非禁用该组件，计时器会继续接收<xref:System.Windows.Forms.Timer.Tick>事件的大致相等的时间间隔。  
  
 此组件专为 Windows 窗体环境设计。 如果需要适合服务器环境的计时器，请参阅[基于服务器的计时器介绍](http://msdn.microsoft.com/library/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。  
  
## <a name="the-interval-property"></a>间隔属性  
 <xref:System.Windows.Forms.Timer.Interval%2A>属性具有几个限制要考虑进行编程时<xref:System.Windows.Forms.Timer>组件：  
  
-   如果你的应用程序或其他应用程序需求很大系统上-例如长循环、 密集型计算或驱动器、 网络或端口访问-你的应用程序可能无法获得的计时器事件，通常为<xref:System.Windows.Forms.Timer.Interval%2A>属性指定。  
  
-   不保证所精确经过的时间间隔。 若要确保准确性，计时器应检查系统时钟根据需要而不是尝试内部跟踪的累积的时间。  
  
-   精度<xref:System.Windows.Forms.Timer.Interval%2A>属性是以毫秒为单位。 某些计算机提供的高分辨率的计数器，分辨率高于毫秒。 这种计数器的可用性取决于你的计算机的处理器硬件。 有关详细信息，请参阅 172338，"如何为使用 QueryPerformanceCounter 到时间的代码，"在 Microsoft 知识库文章在http://support.microsoft.com。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.Timer>  
 [Timer 组件](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)  
 [Timer 组件概述](../../../../docs/framework/winforms/controls/timer-component-overview-windows-forms.md)
