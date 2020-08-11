---
title: Contadores de desempenho para os objetos de desempenho do MSRS 2011 no modo do SharePoint | Microsoft Docs
description: Conheça os contadores de desempenho para os objetos de desempenho do Modo do SharePoint do Serviço Web do MSRS 2011 e do Modo do SharePoint do Serviço Windows do MSRS 2011.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- counters [Reporting Services]
- Report Server Windows service, performance counters
- RS Windows Service performance object
- Scheduling and Delivery Processor performance object [Reporting Services]
- performance [Reporting Services]
ms.assetid: 70bf6980-7845-4ab5-8b2a-ebf526d811a6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 50981b1da0addf5bd55e4640653d3471e3aa459d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545533"
---
# <a name="performance-counters-msrs-2011-sharepoint-mode-performance-objects"></a>Contadores de desempenho para os objetos de desempenho do MSRS 2011 no modo do SharePoint
  Esse tópico descreve os contadores de desempenho para os objetos de desempenho do **modo do SharePoint do Serviço Web MSRS 2011** e do **modo do SharePoint do Serviço do Windows MSRS 2011** que fazem parte da implantação de um modo do SharePoint do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
> [!NOTE]  
>  Esses objetos de desempenho monitoram eventos no servidor de relatório local. Se você estiver executando um servidor de relatório em uma implantação em expansão, as contagens se aplicarão ao servidor atual e não à implantação em expansão como um todo.  
  
 Os objetos de desempenho estão disponíveis no Monitor de Desempenho do Windows (**Perfmon.exe**). Para obter mais informações, consulte a documentação do Windows. [Criação de perfis de runtime](https://msdn.microsoft.com/library/w4bz2147.aspx) (https://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Para obter informações sobre servidores de relatório do modo nativo e contadores de desempenho, consulte [Contadores de desempenho do serviço Web MSRS 2011 e objetos de desempenho do serviço Windows MSRS 2011 &#40;modo nativo&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)[Contadores de desempenho para os objetos de desempenho do serviço do Windows MSRS 2011 e do serviço Web MSRS 2011 (modo do SharePoint)](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
 Neste tópico:  
  
-   [Contadores de desempenho do modo do SharePoint do serviço Web MSRS 2011](#bkmk_webservice)  
  
-   [Contadores de desempenho do modo do SharePoint do serviço do Windows MSRS 2011](#bkmk_windowsservice)  
  
-   [Use cmdlets do PowerShell para retornar listas](#bkmk_powershell)  
  
##  <a name="msrs-2011-web-service-sharepoint-mode-performance-counters"></a><a name="bkmk_webservice"></a> Contadores de desempenho do modo do SharePoint do serviço Web MSRS 2011  
 O objeto de desempenho do **modo do SharePoint do serviço Web MSRS 2011** monitora o desempenho do servidor de relatório. Esse objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por operações interativas de exibição de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] interrompe o serviço Web Servidor de Relatórios.  
  
 A tabela a seguir lista os contadores incluídos com o objeto de desempenho do **modo do SharePoint do serviço Web MSRS 2011** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Sessões ativas**|Número de sessões ativas. Este contador fornece uma contagem cumulativa de todas as sessões de navegador geradas a partir de execuções de relatórios, independentemente de estarem ativas ou não.<br /><br /> O contador é reduzido à medida que os registros de sessão são removidos. Por padrão, as sessões são removidas após dez minutos de inatividade.|  
|**Acertos de cache/s**|Número de solicitações por segundo para relatórios armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte **Total de acertos de cache** mais adiante neste tópico.)|  
|**Acertos do cache/s (modelos semânticos)**|Número de solicitações por segundo para modelos armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache.|  
|**Erros de cache/s**|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Erros do cache/s (modelos semânticos)**|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Solicitações/s da primeira sessão**|Número de sessões de usuário novas que são iniciadas no cache de servidor de relatório a cada segundo.|  
|**Acertos de cache de memória/s**|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Erros de cache de memória/s**|Número de vezes por segundo que os relatórios não puderam ser recuperados do cache na memória.|  
|**Solicitações/s da próxima sessão**|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|**Solicitações de relatório**|Número de relatórios que estão ativos no momento e que estão sendo tratados pelo servidor de relatório.|  
|**Relatórios executados/s**|Número de execuções de relatório bem-sucedidas por segundo. Este contador fornece estatísticas sobre volume de relatório. Use este contador com **Solicitações/s** para comparar a execução de relatórios com solicitações de relatórios que podem ser retornadas do cache.|  
|**Solicitações/s**|Número de solicitações por segundo feitas ao servidor de relatório. Este contador controla todos os tipos de solicitações que são tratadas pelo servidor de relatório.|  
|**Total de acertos de cache**|Número total de solicitações de relatórios do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de acertos do cache (modelos semânticos)**|Número total de solicitações de modelos do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios.|  
|**Total de erros do cache**|Número total de vezes que um relatório não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|**Total de erros do cache (modelos semânticos)**|Número total de vezes que um modelo não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|**Total de acertos do cache de memória**|Número total de relatórios armazenados em cache retornados do cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Total de erros do cache de memória**|Número total de erros de cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de falhas de processamento**|O número de erros de processamento de solicitação no serviço Web Servidor de Relatórios.|  
|**Total de threads rejeitados**|Número total de threads rejeitados para processamento assíncrono e, subsequentemente, tratados como processos síncronos no mesmo thread. Cada fonte de dados é processada em um thread. Se o volume de threads excede à capacidade, os threads serão rejeitados para processamento assíncrono e processados de maneira serial.|  
|**Total de relatórios executados**|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de solicitações**|Número total de todas as solicitações feitas ao servidor de relatório depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
  
##  <a name="msrs-2011-windows-service-sharepoint-mode-performance-counters"></a><a name="bkmk_windowsservice"></a> Contadores de desempenho do modo do SharePoint do serviço do Windows MSRS 2011  
 O objeto de desempenho do **modo do SharePoint do Serviço Windows MSRS 2011** é usado para monitorar o serviço Windows do Servidor de Relatório. Este objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por operações agendadas. As operações agendadas podem incluir assinatura e entrega, instantâneos de execução de relatório e histórico de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas.  
  
 A tabela a seguir lista os contadores incluídos no objeto de desempenho do **modo do SharePoint do Serviço Windows MSRS 2011** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Sessões ativas**|Número de sessões ativas armazenadas no banco de dados do servidor de relatório. Esse contador fornece uma contagem cumulativa de todas as sessões de navegador utilizáveis geradas a partir de assinaturas de relatórios, independentemente de estarem ativas ou não.|  
|**Alerta: comprimento da fila de evento**||  
|**Alerta: eventos processados - CreateSchedule**||  
|**Alerta: eventos processados – excluir agenda**||  
|**Alerta: eventos processados – DeliverAlert**||  
|**Alerta: eventos processados – FireAlert**||  
|**Alerta: eventos processados – FireSchedule**||  
|**Alerta: eventos processados – GenerateAlert**||  
|**Alerta: eventos processados – UpdateSchedule**||  
|**Liberações do cache/s**|Número de liberações de cache por segundo.|  
|**Acertos de cache/s**|Número de solicitações por segundo para relatórios armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte **Total de acertos de cache** mais adiante neste tópico.)|  
|**Acertos do cache/s (modelos semânticos)**|Número de solicitações por segundo para modelos armazenados em cache.|  
|**Erros de cache/s**|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Erros do cache/s (modelos semânticos)**|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Entregas/s**|Número de entregas de relatório por segundo, em qualquer extensão de entrega.|  
|**Eventos/s**|Número de eventos processados por segundo. Os eventos monitorados incluem o **SnapshotUpdated** e o **TimedSubscription**.|  
|**Solicitações/s da primeira sessão**|Número de novas sessões de execução de relatório criadas por segundo.|  
|**Acertos de cache de memória/s**|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Erros de cache de memória/s**|O número de vezes por segundo que os relatórios não podem ser recuperados a partir do cache na memória.|  
|**Solicitações/s da próxima sessão**|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|**Solicitações de relatório**|Número de relatórios que estão ativos no momento e que estão sendo tratados pelo servidor de relatório. Use esse contador para avaliar estratégia de armazenamento em cache. Pode haver significativamente mais solicitações que relatórios gerados.|  
|**Relatórios executados/s**|Número de relatórios gerados com êxito por segundo.|  
|**Solicitações/s**|Número total de solicitações bem-sucedidas do serviço do servidor de relatório processadas por segundo.|  
|**Atualizações de instantâneo/s**|Número total de atualizações de instantâneo de execução de relatório por segundo.|  
|**Total de reciclagens de domínio de aplicativo**|Número total de ciclos do domínio de aplicativo depois do início do serviço Windows do Servidor de Relatório.|  
|**Total de liberações do cache**|Número total de atualizações do cache do servidor de relatórios depois que o serviço é iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Liberações do cache/s**.|  
|**Total de acertos de cache**|Número total de solicitações de relatórios processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Acertos do cache/s**.|  
|**Total de acertos do cache (modelos semânticos)**|Número total de solicitações de modelos processadas diretamente do cache depois do início do serviço Windows do servidor de relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de erros do cache**|Número total de vezes em que não foi possível retornar um relatório do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Erros do cache/s**.|  
|**Total de erros do cache (modelos semânticos)**|Número total de vezes em que não foi possível retornar um modelo do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de entregas**|Número total de relatórios entregues pelo Processador de Agenda e Entrega, para todas as extensões de entrega. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de eventos**|Número total de eventos depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de acertos do cache de memória**|Número total de relatórios armazenados em cache retornados do cache na memória depois do início do serviço Windows do Servidor de Relátório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de erros do cache de memória**|Número total de erros de cache na memória depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de falhas de processamento**|O número de erros de processamento de solicitação para o serviço do Windows servidor de relatórios.|  
|**Total de threads rejeitados**|Número total de threads rejeitados para processamento assíncrono e, subsequentemente, tratados como um processo síncrono no mesmo thread. Com carga moderada ou pesada, esse contador é incrementado continuamente.|  
|**Total de relatórios executados**|Número total de relatórios executados.|  
|**Total de solicitações**|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de atualizações de instantâneos**|Número total de atualizações de instantâneo de execução de relatório.|  
  
##  <a name="use-powershell-cmdlets-to-return-lists"></a><a name="bkmk_powershell"></a> Use cmdlets do PowerShell para retornar listas  
 ![Conteúdo relacionado ao PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")O script do Windows PowerShell a seguir retornará os conjuntos de contadores cujos CounterSetName comecem com "msr"  
  
```  
get-counter -listset msr*  
Returns a list with the following information  
CounterSetName     : MSRS 2011 Windows Service SharePoint Mode  
CounterSetName     : MSRS 2011 Web Service SharePoint Mode  
```  
  
 O script do Windows PowerShell a seguir retornará a lista de contadores de desempenho para o CounterSetName "modo do SharePoint do serviço Windows MSRS 2011".  
  
```  
(get-counter -listset "MSRS 2011 Windows Service SharePoint Mode").paths  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o desempenho do servidor de relatório](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [Contadores de desempenho do serviço Web MSRS 2011 e objetos de desempenho do serviço Windows MSRS 2011 &#40;modo nativo&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Contadores de desempenho para os objetos de desempenho ReportServer:Service e ReportServerSharePoint:Service](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
  
  
