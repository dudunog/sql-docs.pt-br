---
title: Ferramentas de eventos estendidos
description: Essas ferramentas criam e gerenciam sessões de Eventos Estendidos do SQL Server. Além das sessões que você cria, há uma sessão de integridade do sistema padrão no servidor.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fa0e0e6c3b44e07568240d879fdb6d0829e6ffc
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868116"
---
# <a name="extended-events-tools"></a>Ferramentas de eventos estendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Você pode usar as seguintes ferramentas para criar e gerenciar as sessões de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Instruções DLL (linguagem de definição de dados). Elas permitem criar e modificar uma sessão de Eventos Estendidos.  
  
-   Exibições de gerenciamento dinâmico, exibições do catálogo e tabelas do sistema. Elas permitem obter metadados e dados de sessão usando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . Os tabelas do sistema ajudam a determinar os equivalentes existentes dos Eventos Estendidos para classes e colunas de evento do Rastreamento do SQL.  
  
-   O nó **Eventos Estendidos** do Pesquisador de Objetos. Isso permite a você iniciar, interromper ou excluir uma sessão, ou importar e exportar modelos de sessão.  
  
-   O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Essa é uma ferramenta avançada que você pode usar para criar, alterar e gerenciar sessões de Eventos Estendidos. Para obter mais informações, veja [Usar o provedor do PowerShell para Eventos Estendidos](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ela permite criar e executar os exemplos de código fornecidos nos tópicos de Eventos Estendidos. Para obter mais informações, veja [Pesquisador de Objetos](../../ssms/object/object-explorer.md).  
  
 Além das sessões que você cria, há uma sessão de integridade de sistema padrão no servidor. A sessão coleta dados do sistema que você pode usar para ajudar a solucionar problemas de desempenho. Para obter mais informações, veja [Usar a sessão system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="ddl-statements"></a>Instruções DDL  
 Use as instruções DDL a seguir para criar, alterar e remover uma sessão de Eventos Estendidos.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)|Cria um objeto de sessão de Evento Estendido que identifica a origem dos eventos, os destinos da sessão de evento e os parâmetros da sessão de evento.|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)|Inicia ou interrompe uma sessão de evento ou altera uma configuração de sessão de evento.|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)|Remove uma sessão de evento.|  
  
## <a name="catalog-views"></a>Exibições do catálogo  
 Use as exibições do catálogo a seguir para obter os metadados criados quando você cria uma sessão de evento.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|Lista todas as definições de sessão de evento.|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|Retorna uma linha para cada ação em cada evento de uma sessão de eventos.|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|Retorna uma linha para cada evento em uma sessão de eventos.|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|Retorna uma linha para cada coluna personalizável explicitamente definida em eventos e destinos.|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|Retorna uma linha para cada destino de evento em uma sessão de evento.|  
  
## <a name="dynamic-management-views"></a>Exibições de Gerenciamento Dinâmico  
 Use as seguintes exibições de gerenciamento dinâmico para obter metadados e dados de sessão. Os metadados são obtidos nas exibições do catálogo, e os dados de sessão são criados quando você inicia e executa uma sessão de evento.  
  
> [!NOTE]  
>  Estas exibições não contêm dados de sessão até que uma sessão seja iniciada.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|Retorna informações sobre os pools de distribuidores da sessão.|  
|[sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)|Retorna uma linha para cada objeto exposto por um pacote de evento.|  
|[sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)|Retorna as informações de esquema de todos os objetos.|  
|[sys.dm_xe_packages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)|Lista todos os pacotes registrados com o mecanismo de Eventos Estendidos.|  
|[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)|Retorna informações sobre uma sessão de Eventos Estendidos ativa.|  
|[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)|Retorna informações sobre os destinos da sessão.|  
|[sys.dm_xe_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql.md)|Retorna informações sobre os eventos da sessão.|  
|[sys.dm_xe_session_event_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql.md)|Retorna informações sobre ações da sessão de evento.|  
|[sys.dm_xe_map_values &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql.md)|Fornece um mapeamento de chaves numéricas internas para texto legível.|  
|[sys.dm_xe_session_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql.md)|Mostra os valores de configuração de objetos associados a uma sessão.|  
  
## <a name="system-tables"></a>Tabelas do sistema  
 Use as tabelas de sistema a seguir para obter informações sobre os equivalentes de Eventos Estendidos para classes e colunas de evento do Rastreamento do SQL.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)|Contém uma linha para cada evento Eventos Estendidos mapeado para uma classe de evento do Rastreamento do SQL.|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)|Contém uma linha para cada ação de Eventos Estendidos que é mapeada para uma ID de coluna do Rastreamento do SQL.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Tabelas de Eventos Estendidos do SQL Server &#40;Transact-SQL&#41;](../system-tables/system-tables-transact-sql.md)   
 [Usar a sessão system_health](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Usar o provedor do PowerShell para Eventos Estendidos](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
