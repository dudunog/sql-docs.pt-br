---
description: sys.dm_os_memory_cache_hash_tables (Transact-SQL)
title: sys.dm_os_memory_cache_hash_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d40340647e316a42ab7ad047502982da9fe90234
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096546"
---
# <a name="sysdm_os_memory_cache_hash_tables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada cache ativo na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_os_memory_cache_hash_tables**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Endereço (chave primária) da entrada de cache. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Nome do cache. Não permite valor nulo.|  
|**tipo**|**nvarchar(60)**|Tipo de cache. Não permite valor nulo.|  
|**table_level**|**int**|Número da tabela hash. Um cache específico pode ter várias tabelas hash que correspondem a funções hash diferentes. Não permite valor nulo.|  
|**buckets_count**|**int**|Número de partições de memória na tabela hash. Não permite valor nulo.|  
|**buckets_in_use_count**|**int**|Número de partições de memória que estão sendo usadas atualmente. Não permite valor nulo.|  
|**buckets_min_length**|**int**|Número mínimo de entradas de cache em uma partição de memória. Não permite valor nulo.|  
|**buckets_max_length**|**int**|Número máximo de entradas de cache em uma partição de memória. Não permite valor nulo.|  
|**buckets_avg_length**|**int**|Número médio de entradas de cache em cada partição de memória. Não permite valor nulo.|  
|**buckets_max_length_ever**|**int**|Número máximo de entradas em cache em uma partição de memória hash para esta tabela hash, desde que o servidor foi iniciado. Não permite valor nulo.|  
|**hits_count**|**bigint**|Número de acertos do cache. Não permite valor nulo.|  
|**misses_count**|**bigint**|Número de ausências de cache. Não permite valor nulo.|  
|**buckets_avg_scan_hit_length**|**int**|Número médio de entradas examinadas em uma partição de memória antes de um item pesquisado ser localizado. Não permite valor nulo.|  
|**buckets_avg_scan_miss_length**|**int**|Número médio de entradas examinadas em uma partição de memória antes do encerramento sem-êxito da pesquisa. Não permite valor nulo.|  
|**pdw_node_id**|**int**|O identificador do nó em que essa distribuição está.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissões 

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   

## <a name="see-also"></a>Consulte Também  
 
  [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


