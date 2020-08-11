---
title: Usando a classe Setting para uma extensão de entrega | Microsoft Docs
description: Saiba como as extensões de entrega podem usar a classe Setting, que armazena informações de que a extensão de entrega precisa para fornecer notificações e relatórios.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d90728a83821575bd71c3fe93fb1a090beaf8bdb
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529092"
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>Usando a classe Setting para uma extensão de entrega
  A classe <xref:Microsoft.ReportingServices.Interfaces.Setting> está localizada no namespace <xref:Microsoft.ReportingServices.Interfaces> e representa as informações sobre configurações de extensão para uma extensão de entrega. A classe <xref:Microsoft.ReportingServices.Interfaces.Setting> fornece infraestrutura para o armazenamento de informações sobre as configurações obrigatórias para que uma extensão de entrega funcione corretamente. Por exemplo, na entrega de E-Mail do Report Server, é necessário que um usuário forneça configurações específicas de entrega de e-mails, como o endereço do destinatário, o endereço do remetente, a linha de assunto do e-mail e mais. Indubitavelmente, os seus provedores de entrega personalizados exigirão que o usuário forneça configurações específicas para que a extensão de entrega entregue notificações e relatórios.  
  
 A classe de <xref:Microsoft.ReportingServices.Interfaces.Setting> é usada na implementação da propriedade de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> da interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. A classe de <xref:Microsoft.ReportingServices.Interfaces.Setting> também é usada para o processamento dos dados de configuração da extensão fornecidos por um usuário quando uma assinatura ou notificação é criada.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.Setting>, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
