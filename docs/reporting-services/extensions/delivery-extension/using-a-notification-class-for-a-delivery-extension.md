---
title: Usando uma classe de notificação para uma extensão de entrega | Microsoft Docs
description: Descubra como as extensões de entrega podem usar a classe Notification. Essa classe armazena informações de assinatura usadas durante a entrega de relatórios.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 20f65f0aeb5e7ab9a74da2b1f3baae574c45f3f2
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529472"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>Usando uma classe de notificação classe para uma extensão de entrega
  A classe <xref:Microsoft.ReportingServices.Interfaces.Notification> classe está localizada no namespace <xref:Microsoft.ReportingServices.Interfaces> e representa informações de assinatura que extensões de entrega usam para entregar relatórios. A classe <xref:Microsoft.ReportingServices.Interfaces.Notification> oferece algumas propriedades que podem ser usadas para renderizar os relatórios para entrega, determinar o status da notificação e definir dados de usuário.  
  
 ![Processo de notificação de relatório](../../../reporting-services/extensions/delivery-extension/media/bk-ext-03.gif "Processo de notificação de relatório")  
A notificação é o objeto central de qualquer entrega  
  
 Quando um evento dispara que está associado a uma assinatura que usa a sua extensão de entrega personalizada, uma notificação com um objeto <xref:Microsoft.ReportingServices.Interfaces.Report> será criada. O objeto <xref:Microsoft.ReportingServices.Interfaces.Report> encapsula a funcionalidade necessária para a renderização de um determinado relatório para um formato de renderização suportado e contém propriedades específicas do relatório, como a URL para o relatório no servidor e o nome do relatório. Para obter mais informações sobre a classe <xref:Microsoft.ReportingServices.Interfaces.Report>, consulte [Usando a classe Report para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md).  
  
 Você passa o objeto <xref:Microsoft.ReportingServices.Interfaces.Notification> ao método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de sua extensão de entrega. Seu método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> deve conter código específico para processar a notificação e entregar o relatório.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.Notification>, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="retry-functionality"></a>Funcionalidade de repetição  
 O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite a você criar uma fila de repetição para notificações que não podem ser entregues imediatamente. Depois que o servidor de relatório invoca o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de uma extensão de entrega, a extensão de entrega poderá solicitar que o servidor de relatório tente entregar novamente em um momento determinado. Se isso acontecer, o servidor de relatório coloca a notificação em uma fila interna e tenta entregar novamente após um período de tempo específico. Os administradores podem configurar o número máximo de novas tentativas executadas pelo servidor de relatório e o período entre as novas tentativas na seção da extensão de entrega do arquivo RSReportServer.config usando o elemento XML **MaxNumberOfRetries** e o elemento XML **PeriodBetweenRetries**. As notificações são removidas da fila de repetição se a entrega for bem-sucedida mais tarde ou se o número máximo de novas tentativas for alcançado. Se a entrega falhar depois do número de máximo de novas tentativas, a notificação será descartada.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
