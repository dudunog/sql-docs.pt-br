---
title: Alterar a extensão de entrega padrão do Reporting Services | Microsoft Docs
description: Saiba como definir as configurações do Reporting Services para reorganizar as extensões de entrega mostradas na lista "Entregue por" e definir a extensão de entrega padrão.
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 83c2c0c6bb3c2a457182e8dcf56c5caa68397184
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80742307"
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>Alterar a extensão de entrega padrão do Reporting Services
  Você pode modificar as definições de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para alterar a extensão de entrega padrão que aparece na lista **Entregue por** de uma página de definição de assinatura. Por exemplo, você pode modificar a configuração de modo que quando os usuários criem uma nova assinatura, a entrega de compartilhamento de arquivos seja selecionada por padrão, em vez da entrega de email. Você também pode alterar a ordem em que as extensões de entrega são listadas na interface do usuário.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui as entregas de Email e Compartilhamento de Arquivos do Windows como extensões. O servidor de relatório pode ter extensões de entrega adicionais caso extensões personalizadas ou de terceiros tenham sido implantadas para oferecer suporte à entrega personalizada. A disponibilidade de uma extensão de entrega depende de sua implantação em um servidor de relatório.  
  
## <a name="default-native-mode-report-server-configuration"></a>Configuração padrão de servidor de relatório em modo nativo  
 A ordem de uma extensão de entrega que aparece no Report Manager na lista **Entregue por** baseia-se na ordem das entradas de extensão de entrega do arquivo **RSReportServer.config** . Por exemplo, a imagem a seguir mostra email em primeiro lugar na lista e é selecionada por padrão.  
  
 ![lista padrão de extensões de entrega](../../reporting-services/subscriptions/media/ssrs-default-delivery.png "lista padrão de extensões de entrega")  
  
 A seguir está a seção padrão de **RSReportServer.config** , que controla a extensão de entrega padrão e a ordem em que elas são exibidas no Gerenciador de relatórios. Observe que o email aparece primeiro no arquivo e é definido como o padrão.  
  
```  
<DeliveryUI>  
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
               <Configuration>  
               <RSEmailDPConfiguration>  
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
               </RSEmailDPConfiguration>  
               </Configuration>  
     </Extension>  
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>  
</DeliveryUI>  
```  
  
#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>Configure a entrega de compartilhamento de arquivos como a extensão de entrega padrão no Gerenciador de Relatórios  
  
1.  As etapas neste procedimento modificam a configuração para que a entrega de compartilhamento de arquivos seja listada como a primeira opção na interface do usuário e seja a seleção padrão.  
  
     Abra o arquivo RSReportServer.config em um editor de texto. Para obter mais informações sobre o arquivo de configuração, consulte [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). Após a configuração ter sido alterada, a interface do usuário será semelhante à imagem a seguir:  
  
     ![lista modificada de extensões de entrega](../../reporting-services/subscriptions/media/ssrs-modified-delivery.png "lista modificada de extensões de entrega")  
  
2.  Modifique a seção DeliveryUI para se parecer com o exemplo a seguir e observe as principais alterações:  
  
    1.  A extensão de compartilhamento de arquivos fica antes da extensão de email. Isso vai alterar a ordem em que as extensões são listadas no Gerenciador de Relatórios.  
  
    2.  A extensão de compartilhamento de arquivos contém a marca DefaultExtension `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` e a marca de fim de extensão `</Extension>`foi adicionada.  
  
    3.  A extensão de email não está mais configurada como o padrão. `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`  
  
    ```  
    <DeliveryUI>  
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">  
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
         </Extension>  
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>  
         <Configuration>  
              <RSEmailDPConfiguration>  
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
              </RSEmailDPConfiguration>  
         </Configuration>  
         </Extension>  
    </DeliveryUI>  
    ```  
  
3.  Salve o arquivo de configuração.  
  
4.  Em alguns minutos, o servidor de relatório recarregará o arquivo de configuração e as novas configurações se efetivarão. Você pode reiniciar o serviço do servidor de relatório para forçar o carregamento do arquivo de configuração.  
  
     O evento a seguir é gravado no log de eventos do Windows quando a configuração é lida.  
  
     **ID de evento:** 109  
  
     **Fonte:** Serviço Windows do Servidor de Relatórios (nome da instância)  
  
     O arquivo RSReportServer.config foi modificado  
  
## <a name="sharepoint-mode-report-servers"></a>Servidores de relatório no modo do SharePoint  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo do SharePoint armazena informações de extensões nos bancos de dados de aplicativo do serviço SharePoint e não no arquivo RsrReportServer.config. No modo do SharePoint, a configuração de extensão de entrega é modificada usando o PowerShell.  
  
#### <a name="configure-the-default-delivery-extension"></a>Configurar a extensão de entrega padrão  
  
1.  Abra o **Shell de Gerenciamento do SharePoint**.  
  
2.  Você poderá ignorar esta etapa se já souber o nome do seu aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use o PowerShell a seguir para listar os aplicativos de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no seu farm do SharePoint.  
  
    ```  
    get-sprsserviceapplication | format-list *  
    ```  
  
3.  Execute o PowerShell a seguir para verificar a extensão de entrega padrão atual para o aplicativo de serviço "ssrsapp" do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    ```  
    $app=get-sprsserviceapplication | where {$_.name -like "ssrsapp*"};Get-SPRSExtension -identity $app | where{$_.ServerDirectivesXML -like "<DefaultDelivery*"} | format-list *  
  
    ```
  
## <a name="see-also"></a>Consulte Também  
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Entrega de compartilhamento de arquivos no Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Entrega de email no Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   

