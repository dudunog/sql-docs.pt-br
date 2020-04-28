---
title: 'Contadores de desempenho para os objetos de desempenho ReportServer: Service e ReportServerSharePoint: Service | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Server service, performance counters
ms.assetid: 2bcacab2-3a4f-4aae-b123-19d756b9b9ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca5a4561c4b3f55044eb63068036105d878f150c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175063"
---
# <a name="performance-counters-for-the-reportserverservice--and-reportserversharepointservice-performance-objects"></a>Performance Counters for the ReportServer:Service  and ReportServerSharePoint:Service Performance Objects
  Este tópico descreve os contadores de desempenho dos seguintes objetos de desempenho do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] :

-   `ReportServer:Service`

-   `ReportServerSharePoint:Service`

> [!NOTE]
>  Os objetos de desempenho são usados para monitorar eventos no servidor de relatório local. Se você estiver executando um servidor de relatório em uma implantação em expansão, as contagens se aplicarão ao servidor atual e não à implantação em expansão como um todo.

 Os objetos de desempenho estão disponíveis no Monitor de Desempenho do Windows (**Perfmon.exe**). Para obter mais informações, consulte a documentação do Windows. [Criação de perfis de runtime](https://msdn.microsoft.com/library/w4bz2147.aspx) (https://msdn.microsoft.com/library/w4bz2147.aspx).

 Neste tópico:

-   [Contadores de Desempenho ReportServer:Service (servidor de relatório no modo nativo)](#bkmk_ReportServer)

-   [ReportServerSharePoint:serviço (servidor de relatório no modo do SharePoint)](#bkmk_ReportServerSharePoint)

-   [Use cmdlets do PowerShell para retornar listas](#bkmk_powershell)

 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo do SharePoint | Modo nativo.

##  <a name="reportserverservice-performance-counters-native-mode-report-server"></a><a name="bkmk_ReportServer"></a> Contadores de Desempenho ReportServer:Service (servidor de relatório no modo nativo)
 O objeto de desempenho `ReportServer:Service` inclui uma coleção de contadores a fim de controlar os eventos relativos ao HTTP e à memória de uma instância do servidor de relatório. Esse objeto aparece uma vez para cada instância do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no computador, e é possível adicionar ou remover contadores do objeto para cada instância. Os contadores da instância padrão aparecem no formato `ReportServer:Service`. Os contadores para instâncias nomeadas aparecem no `ReportServer$<`formato *instance_name*`>:Service`.

 O `ReportServer:Service` objeto de desempenho era novo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]no e fornece um subconjunto de contadores que foram incluídos com serviços de informações da Internet (IIS) e [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] em versões anteriores do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Esses novos contadores são específicos do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]e controlam eventos relacionados ao HTTP do servidor de relatório, como solicitações, conexões e tentativas de logon. Adicionalmente, ele inclui contadores para controlar eventos de gerenciamento de memória.

 A tabela a seguir lista os contadores incluídos no objeto de desempenho `ReportServer:Service`.

 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") O script do Windows PowerShell a seguir retornará a lista de contadores de desempenho para o CounterSetName

```
(get-counter -listset "ReportServer:Service").paths
```

|Contador|DESCRIÇÃO|
|-------------|-----------------|
|`Active connections`|O número de conexões atualmente ativas no servidor.|
|`Bytes Received Total`|O número de bytes recebidos pelo servidor. Esse contador calcula o total de bytes brutos recebidos pelo Gerenciador de Relatórios e pelo servidor de relatório.|
|`Bytes Received/sec`|O número de bytes recebidos por segundo pelo servidor. Esse contador é atualizado apenas quando uma transferência é concluída. Isso significa que o contador permanece em 0 e o valor só é alterado depois da conclusão de uma transferência.|
|`Bytes Sent Total`|O número de bytes enviados do servidor. Esse contador calcula o total de bytes brutos enviados pelo Gerenciador de Relatórios e pelo servidor de relatório.|
|`Bytes Sent/sec`|O número de bytes enviados por segundo pelo servidor. Esse contador é atualizado apenas quando uma transferência é concluída. Isso significa que o contador permanece em 0 e o valor só é alterado depois da conclusão de uma transferência.|
|`Errors Total`|O número total de erros durante o processamento das solicitações HTTP. Esses erros incluem os códigos de status do HTTP 400s e 500s.|
|`Errors/sec`|O número total de erros por segundo durante o processamento das solicitações HTTP. Esses erros incluem os códigos de status do HTTP 400s e 500s.|
|`Logon Attempts Total`|O número de tentativas de logon feitas com os tipos de autenticação RSWindows. Os tipos de autenticação RSWindows incluem RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos e RSWindowsBasic. O valor zero (0) representa a autenticação personalizada.|
|`Logon Attempts/sec`|A taxa de tentativas de logon.|
|`Logon Successes Total`|O número de logons bem-sucedidos para os tipos de autenticação RSWindows. Os tipos de autenticação RSWindows incluem RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos e RSWindowsBasic. O valor zero (0) representa a autenticação personalizada.|
|`Logon Successes/sec`|A taxa de logons bem-sucedidos.|
|`Memory Pressure State`|Um dos números (1-5) a seguir indica o estado atual da memória do servidor:<br /><br /> 1: Nenhuma pressão<br /><br /> 2: Baixa pressão<br /><br /> 3: Média pressão<br /><br /> 4: Alta pressão<br /><br /> 5: Excesso de pressão|
|`Memory Shrink Amount`|O número de bytes que devem ser reduzidos na memória em uso devido à solicitação do servidor.|
|`Memory Shrink Notifications/sec`|O número de notificações que o servidor emitiu no último segundo para reduzir a memória em uso. Esse valor indica com que frequência a memória do servidor está sob pressão.|
|`Requests Disconnected`|O número de solicitações desconectadas por causa de uma falha de comunicação.|
|`Requests Executing`|O número de solicitações em processamento no momento.|
|`Requests Not Authorized`|O número de solicitações que falham com o código de status do HTTP 401.|
|`Requests Rejected`|O número total de solicitações não processadas por causa de recursos de servidor insuficientes. Esse contador representa o número de solicitações que retornam o código de status do HTTP 503, o qual indica que o servidor está muito ocupado.|
|`Requests Total`|O número total de solicitações recebidas pelo serviço de servidor de relatório desde a inicialização. Esse contador calcula as solicitações enviadas para o Gerenciador de Relatórios e as enviadas do Gerenciador de Relatórios para o servidor de relatório.|
|`Requests/sec`|O número de solicitações processadas por segundo. Esse valor representa a taxa de transferência atual do aplicativo.|
|`Tasks Queued`|O número de tarefas que estão esperando um thread para se tornarem disponíveis para processamento. Cada solicitação feita ao servidor de relatório corresponde a uma ou mais tarefas. Esse contador representa apenas o número de tarefas que estão prontas para processamento; ele não inclui o número de tarefas atualmente em execução.|

##  <a name="reportserversharepointservice-sharepoint-mode-report-server"></a><a name="bkmk_ReportServerSharePoint"></a> ReportServerSharePoint:serviço (servidor de relatório no modo do SharePoint)
 O `ReportServerSharePoint:Service` objeto de desempenho foi adicionado [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]no.

 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") O script do Windows PowerShell a seguir retornará a lista de contadores de desempenho para o CounterSetName

```
(get-counter -listset "ReportServerSharePoint:Service").paths
```

|Contador|
|-------------|
|`Memory Pressure State`|
|`Memory Shrink Amount`|
|`Memory Shrink Notifications/Sec`|

##  <a name="use-powershell-cmdlets-to-return-lists"></a><a name="bkmk_powershell"></a>Usar cmdlets do PowerShell para retornar listas
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") O seguinte script do Windows PowerShell retornará a lista de contadores de desempenho para o CounterSetName "ReportServerSharePoint:Service":

```
(get-counter -listset "ReportServerSharePoint:Service").paths
```

## <a name="see-also"></a>Consulte Também
 [Monitorando](monitoring-report-server-performance.md) [contadores de desempenho de desempenho do servidor de relatório para o serviço Web MSRS 2014 e objetos de desempenho do serviço Windows MSRS 2014 &#40;modo nativo&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md) [contadores de desempenho para o modo do SharePoint do serviço Web MSRS 2014 e objetos de desempenho do modo do SharePoint do serviço Windows MSRS 2014 &#40;modo do SharePoint&#41;].. /performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)


