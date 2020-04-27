---
title: Monitorando e Solucionando problemas de objetos de banco de dados gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f03266a5460e9e34a404256e5df415f799b29d98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918928"
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>Monitorando e diagnosticando objetos de banco de dados gerenciado
  Este tópico fornece informações sobre as ferramentas que podem ser usadas para monitorar e diagnosticar objetos de banco de dados gerenciado e assemblies executados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="profiler-trace-events"></a>Eventos de rastreamento do Profiler  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece o Rastreamento do SQL e notificações de eventos para monitorar os eventos que ocorrem no Mecanismo de Banco de Dados. Registrando os eventos especificados, o Rastreamento do SQL ajuda a solucionar problemas de desempenho, auditar a atividade de banco de dados, coletar dados de amostra em um ambiente de teste, depurar instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] e procedimentos armazenados e reunir dados para ferramentas de análise de desempenho. Para obter mais informações, consulte [rastreamento do SQL](../sql-trace/sql-trace.md) e [eventos estendidos](../extended-events/extended-events.md).  
  
|Evento|Descrição|  
|-----------|-----------------|  
|[Classe de evento Assembly Load](../../database-engine/assembly-load-event-class.md)|Usado para monitorar solicitações de carregamento de assembly (com êxito e com falha).|  
|Classe de evento [SQL: BatchStarting](../event-classes/sql-batchstarting-event-class.md), [classe de evento SQL: BatchCompleted](../event-classes/sql-batchcompleted-event-class.md)|Fornece informações sobre lotes [!INCLUDE[tsql](../../../includes/tsql-md.md)] iniciados ou concluídos.|  
|Classe de evento [SP: Starting](../event-classes/sp-starting-event-class.md), [SP: Completed](../event-classes/sp-completed-event-class.md)|Usado para monitorar a execução de procedimentos armazenados [!INCLUDE[tsql](../../../includes/tsql-md.md)].|  
|Classe de evento [SQL: StmtStarting](../event-classes/sql-stmtstarting-event-class.md), [classe de evento SQL: StmtCompleted](../event-classes/sql-stmtcompleted-event-class.md)|Usado para monitorar a execução de CLR e rotinas [!INCLUDE[tsql](../../../includes/tsql-md.md)].|  
  
## <a name="performance-counters"></a>Contadores de desempenho  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor do Sistema para monitorar a atividade em computadores que executem uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Um objeto é qualquer recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como um bloqueio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um processo do Windows. Cada objeto contém um ou mais contadores, que determinam vários aspectos dos objetos a monitorar. Para obter mais informações, confira o artigo [Usar objetos do SQL Server](../performance-monitor/use-sql-server-objects.md).  
  
|Objeto|Descrição|  
|------------|-----------------|  
|[SQL Server, objeto CLR](../performance-monitor/sql-server-clr-object.md)|Tempo total gasto na execução de CLR.|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Contadores do Monitor do Sistema do Windows (PERFMON.EXE)  
 A ferramenta Monitor do Sistema do Windows (PERFMON.EXE) tem vários contadores de desempenho que podem ser usados para monitorar aplicativos de integração CLR. Os contadores de desempenho CLR do .NET podem ser filtrados pelo nome do processo "sqlservr" para rastrear aplicativos de integração CLR que estão em execução no momento.  
  
|Objeto de Desempenho|Descrição|  
|------------------------|-----------------|  
|SqlServer:CLR|Fornece estatísticas de CPU para o servidor.|  
|Exceções .NET CLR|Rastreia o número de exceções por segundo.|  
|Carregamento de .NET CLR|Fornece informações sobre o AppDomains e os assemblies carregados no servidor.|  
|Memória de .NET CLR|Fornece informações sobre o uso da memória de CLR. Este objeto poderá ser usado para sinalizar alertará se o uso da memória se tornar muito intenso.|  
|Provedor de Dados .Net para SQL Server|Rastreia o número de conexões e desconexões por segundo. Este objeto pode ser usado para monitorar o nível de atividade do banco de dados.|  
  
## <a name="catalog-views"></a>Exibições do catálogo  
 As exibições de catálogo retornam informações usadas pelo Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Recomendamos usar exibições do catálogo por serem a interface mais geral para metadados de catálogo e proporcionarem a maneira mais eficaz de obter, transformar e apresentar formas personalizadas dessas informações. Todos os metadados de catálogos disponíveis para o usuário são expostos por meio de exibições do catálogo. Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql).  
  
|Exibição de catálogo|Descrição|  
|------------------|-----------------|  
|[sys.assemblies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)|Retorna informações sobre os assemblies registrados em um banco de dados.|  
|[sys.assembly_references &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)|Identifica os assemblies que referenciam outros.|  
|[sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)|Retorna informações sobre cada função, procedimento armazenado e gatilho definidos em um assembly.|  
|[sys.assembly_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)|Retorna informações sobre os arquivos de assembly registrados em um banco de dados.|  
|[sys.assembly_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)|Identifica os UDTs (tipos definidos pelo usuário) definidos por um assembly.|  
|[sys.module_assembly_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql)|Identifica os assemblies nos quais os módulos CLR estão definidos.|  
|[sys.parameter_type_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)|Retorna informações sobre parâmetros que são UDTs.|  
|[sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)|Identifica o assembly no qual um gatilho CLR está definido.|  
|[sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)|Identifica os gatilhos DDL de nível de servidor em um servidor, inclusive gatilhos CLR.|  
|[sys.type_assembly_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql)|Identifica os assemblies nos quais os UDTs estão definidos.|  
|[sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)|Retorna o sistema e os UDTs registrados no banco de dados.|  
  
## <a name="dynamic-management-views"></a>Exibições de Gerenciamento Dinâmico  
 As exibições e funções de gerenciamento dinâmico retornam informações do estado do servidor que podem ser usadas para monitorar a saúde da instância do servidor, diagnosticar problemas e ajustar o desempenho. Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](../views/views.md).  
  
|DMV|Descrição|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)|Fornece informações sobre cada domínio do aplicativo no servidor.|  
|[sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql)|Identifica cada assembly gerenciado registrado no servidor.|  
|[sys.dm_clr_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql)|Retorna informações sobre o CLR hospedado.|  
|[sys.dm_clr_tasks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql)|Identifica todas as tarefas CLR que estão em execução no momento.|  
|[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)|Retorna informações sobre os planos de execução de consultas armazenados em cache pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para agilizar a execução de consultas.|  
|[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)|Retorna estatísticas de desempenho de agregação dos planos de consulta em cache.|  
|[sys.dm_exec_requests &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql)|Retorna informações sobre cada solicitação sendo executada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)|Retorna todos os administradores de memória ativos no momento na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], incluindo administradores de memória CLR.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
