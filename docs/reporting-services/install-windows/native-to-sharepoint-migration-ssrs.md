---
description: Migração do modo nativo para o SharePoint (SSRS)
title: Migração do modo nativo para o SharePoint | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016
ms.openlocfilehash: f6020b7c7288ff9ed5a31e345dc26b06a07071bf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439331"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>Migração do modo nativo para o SharePoint (SSRS)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Você não pode atualizar ou converter de um modo de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para outro. Por exemplo, você não pode atualizar ou converter um servidor de relatório de modo nativo para um modo do SharePoint. Você não pode copiar os bancos de dados de servidor de relatório entre modos porque eles usam esquemas de banco de dados diferentes. Você pode migrar o conteúdo de um servidor de relatório para outro. As ferramentas que você usa dependem do tipo de modo do servidor de relatório configurado para os servidores de origem e destino.  
  
##  <a name="reporting-services-migration-tool"></a><a name="bkmk_native_to_sharepoint"></a> Ferramenta de migração do Reporting Services  
 A ferramenta oferece suporte à migração de conteúdo de uma implantação de modo nativo para uma implantação do modo do SharePoint. A ferramenta não oferece suporte à migração do modo do SharePoint para o modo do SharePoint ou do modo do SharePoint para o modo nativo.  
  
 Para saber mais, veja [Ferramenta de migração do Reporting Services](https://www.microsoft.com/download/details.aspx?id=29560) (https://www.microsoft.com/download/details.aspx?id=29560).  
  
## <a name="use-script-to-migrate-content"></a>Use o script para migrar conteúdo  
 Se a ferramenta de migração não atender às suas necessidades, você poderá migrar manualmente os dados do servidor de relatório. Veja a seguir um resumo das etapas a serem concluídas para migrar itens de relatório de uma implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para outra. A abordagem oferece suporte ao modo nativo ou o modo do SharePoint como os servidores de origem ou destino.  
  
1.  Fazer backup e restaurar chaves de criptografia. Esta é a chave usada para criptografar dados. A chave de criptografia também é usada para criptografar senhas como as senhas armazenadas para conexões da fonte de dados. Porém, as senhas não podem ser migradas e você precisará inscrevê-las novamente no ambiente de destino.  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Scripts RSS:** grave um script do Visual Basic que chame os métodos SOAP do serviço Web Servidor de Relatórios para copiar dados entre os bancos. Use o utilitário **RS.exe** para executar o script. O RS.exe é instalado com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    -   [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md). Os tópicos a seguir explicam como usar o script de exemplo que você pode baixar do CodePlex.  
  
    -   O script rss de exemplo no CodePlex, [Script RS.exe do Reporting Services que migra o conteúdo de um servidor de relatório para outro](https://azuresql.codeplex.com/releases/view/115207).  
  
    -   [Script e PowerShell com o Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)  
  
 A tabela a seguir resume os objetos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você pode migrar com scripts:  
  
|Objeto|Pode ser gerado por script|Comentários|  
|------------|---------------------|--------------|  
|Relatórios|Sim|Após a migração, reinsira senhas para fontes de dados.|  
|Fontes de dados|Sim|Após a migração, revincule relatórios a fontes de dados.|  
|Modelos|Sim||  
|Conjunto de dados|Sim||  
|Partes de relatório||Após a migração, verifique ou atualize o caminho para as partes de relatório.|  
|Agendas|Sim|Consulte o método ListSchedules [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|  
|Assinaturas|sim|Veja o método [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md) de List Subscriptions e o método <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> .|  
|Instantâneos|||

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
