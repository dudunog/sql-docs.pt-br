---
title: Implementando a interface IDeliveryExtension para uma extensão de entrega | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 229d08da8be91a462b243fbb5580395fd03867ed
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193637"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementando a interface IDeliveryExtension para uma extensão de entrega
  A sua classe de extensão de entrega é usada para entregar notificações de relatório a usuários com base no conteúdo das notificações. A classe de extensão de entrega também oferece infraestrutura para validar configurações de usuário passadas à extensão de entrega. Além disso, a sua classe de extensão de entrega deve conter propriedades específicas que os clientes poderão usar para obter informações sobre o nome da extensão, as configurações suportadas pela extensão e os formatos disponíveis para a extensão de entrega.  
  
 ![Processo de interface IDeliveryExtension](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "Processo de interface IDeliveryExtension")  
A interface IDeliveryExtension permite a validação de dados de usuário como também de clientes para aprender sobre as configurações de entrega exigidas  
  
 Para criar uma classe de extensão de entrega, implemente <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>. A interface **IDeliveryExtension** permite que a extensão de entrega forneça notificações de relatório usando o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> e valide as configurações de extensão de entrada usando o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>. A interface **IExtension** permite que você habilite a extensão de entrega para implementar um nome de extensão localizado e processe informações de configuração específicas à extensão armazenadas no arquivo de configuração [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ao implementar **IExtension**, a extensão de entrega conterá a propriedade <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>. É altamente recomendável que as extensões de entrega do [!INCLUDE[ssRS](../../../includes/ssrs.md)] deem suporte à propriedade **LocalizedName**, para que os usuários encontrem um nome conhecido para a extensão em uma interface do usuário, como Gerenciador de Relatórios.  
  
 A extensão de entrega também deve implementar a propriedade **ExtensionSettings** da interface **IDeliveryExtension**. O servidor de relatório usa o valor retornado pela propriedade <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> para avaliar as configurações exigidas por uma extensão de entrega. Os clientes que interagem com extensões de entrega usam o método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> do serviço Web Servidor de Relatório para retornar uma lista de configurações para a extensão de entrega.  
  
 Você também pode usar a sua classe de extensão de entrega para recuperar e processar dados de configuração personalizados armazenados no arquivo RSReportServer.config. Para obter mais informações sobre como processar dados de configuração personalizados, consulte o método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Para obter uma implementação da classe **IDeliveryExtension** de exemplo, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
