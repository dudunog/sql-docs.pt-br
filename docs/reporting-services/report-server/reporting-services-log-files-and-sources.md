---
title: Fontes e arquivos de log do Reporting Services | Microsoft Docs
ms.date: 05/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a0f6270fc40d4a22db2d8b03deba8a53e57fbf6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65620317"
---
# <a name="reporting-services-log-files-and-sources"></a>Fontes e arquivos de log do Reporting Services
  Um servidor de relatório e um ambiente de servidor de relatório usam uma variedade de destinos de log para registrar informações sobre operações e status do servidor. Há duas categorias básicas de registro em log, log de execução e log de rastreamento. O log de execução inclui informações sobre estatística de execução de relatório, auditoria, diagnóstico de desempenho e otimização. O log de rastreamento são informações sobre mensagens de erro e diagnóstico em geral.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 A tabela a seguir fornece links para informações adicionais sobre cada log, incluindo o local e como exibir seu conteúdo.  
  
|Log|DESCRIÇÃO|  
|---------|-----------------|  
|[ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)|O log de execução é um modo de exibição do SQL Server armazenado no banco de dados do servidor de relatório.<br /><br /> O log de execução do servidor de relatório contém dados sobre relatórios específicos, incluindo quando o relatório foi executado, quem o executou, quando foi entregue e qual formato de renderização foi usado.|  
|Log de rastreamento do SharePoint|Para servidores de relatório executados no SharePoint, os logs de rastreamento do SharePoint contêm informações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você também pode configurar as informações específicas do [!INCLUDE[ssRS](../../includes/ssrs.md)] para o serviço de log unificado do SharePoint. Para obter mais informações, consulte [Ativar eventos do Reporting Services para o log de rastreamento do SharePoint &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[Log de rastreamento do serviço Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md)|O log de rastreamento de serviço contém informações bem detalhadas que são úteis se você estiver depurando um aplicativo ou investigando um problema ou evento. Os arquivos de log de rastreamento são ReportServerService_\<timestamp>.log e estão localizados na seguinte pasta:<br /><br /> No SQL Server Reporting Services 2016 ou anteriores: `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`<br /><br /> No SQL Server Reporting Services 2017: `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles`|  
|[Log HTTP do Servidor de Relatório](../../reporting-services/report-server/report-server-http-log.md)|O arquivo de log HTTP contém um registro de todas as solicitações e respostas HTTP manipuladas pelo serviço Web do servidor de relatório.|  
|[Log de aplicativo do Windows](../../reporting-services/report-server/windows-application-log.md)|O log de aplicativos de Microsoft Windows contém informações sobre eventos de servidor de relatório.|  
|Logs de desempenho do Windows|Os logs de desempenho do Windows contêm dados de desempenho do servidor de relatório. Você pode criar logs de desempenho e escolher contadores que determinam quais dados devem ser coletados. Para obter mais informações, consulte [Monitoramento do Desempenho do Servidor de Relatório](../../reporting-services/report-server/monitoring-report-server-performance.md).|  
|Arquivos de log de Instalação do SQL Server|Arquivos de log também são criados durante a instalação. Se a instalação falhar ou for bem-sucedida com avisos ou outras mensagens, você poderá examinar os arquivos de log para solucionar o problema. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).|  
|Logs IIS|Arquivos de log criados por Serviços de Informações da Internet da Microsoft (IIS). Para saber mais, veja [Como habilitar o log em Serviços de Informações da Internet (IIS)](https://support.microsoft.com/kb/313437) (https://support.microsoft.com/kb/313437).|  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
