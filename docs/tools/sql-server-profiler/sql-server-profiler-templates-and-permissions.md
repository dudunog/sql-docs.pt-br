---
title: Modelos e permissões do SQL Server Profiler
titleSuffix: SQL Server Profiler
description: Saiba como o SQL Server Profiler funciona, como usá-lo para rastrear eventos e onde encontrar mais informações sobre seus recursos.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 96c78bc0fee624170b94b3360f75e00d876dc218
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729563"
---
# <a name="sql-server-profiler-templates-and-permissions"></a>Modelos e permissões do SQL Server Profiler

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] mostra como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resolve consultas internamente. Isso permite que os administradores saibam exatamente quais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ou Expressões Multidimensionais são enviadas ao servidor e como este acessa o banco de dados ou cubo para retornar conjuntos de resultados.  
  
 Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode fazer este procedimento:  
  
-   Criar um rastreamento baseado em um modelo reutilizável  
  
-   Observar os resultados do rastreamento enquanto ele é executado  
  
-   Armazenar os resultados do rastreamento em uma tabela  
  
-   Iniciar, interromper, pausar e modificar os resultados do rastreamento, conforme a necessidade  
  
-   Repetir os resultados do rastreamento  
  
 Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar apenas os eventos que lhe interessam. Se os rastreamentos estiverem se tornando grandes demais, você poderá filtrá-los de acordo com as informações desejadas, de modo que apenas um subconjunto dos dados do evento seja coletado. O monitoramento de muitos eventos causa sobrecarga no servidor e no processo de monitoramento, além de aumentar muito a tabela ou arquivo de rastreamento, especialmente se o monitoramento se estender por um longo período de tempo.  
  
> [!NOTE]  
>  Os valores de coluna de rastreamento maiores que 1 GB retornam um erro e são truncados na saída do rastreamento.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Modelos do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates.md)|Contém informações sobre os modelos de rastreamento predefinidos que acompanham o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|Contém informações sobre as permissões exigidas para executar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Salvar rastreamentos e modelos de rastreamento](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|Contém informações sobre como salvar a saída do rastreamento e como salvar as definições de rastreamento em um modelo.|  
|[Modificar modelos de rastreamento](../../tools/sql-server-profiler/modify-trace-templates.md)|Contém informações sobre como modificar modelos de rastreamento usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|[Iniciar um rastreamento](../../tools/sql-server-profiler/start-a-trace.md)|Contém informações sobre o que acontece quando um rastreamento é iniciado, pausado ou interrompido.|  
|[Correlacionar um rastreamento com os dados de log de desempenho do Windows](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|Contém informações sobre como correlacionar os dados do log de desempenho do Windows com um rastreamento, usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler.|  
|[Exibir e analisar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|Contém informações sobre como usar rastreamentos para solucionar problemas de dados, como exibir nomes de objeto em um rastreamento e como localizar eventos em um rastreamento.|  
|[Analisar deadlocks com o SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|Contém informações sobre como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para identificar a causa de um deadlock.|  
|[Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|Contém informações sobre como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para coletar e exibir resultados do Plano de Execução e suas estatísticas.|  
|[Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|Contém informações sobre como definir filtros em colunas de dados para filtrar a saída do rastreamento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Reproduzir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)|Contém informações que explicam o que significa repetir um rastreamento e o que é necessário para isso.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Iniciar o SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
