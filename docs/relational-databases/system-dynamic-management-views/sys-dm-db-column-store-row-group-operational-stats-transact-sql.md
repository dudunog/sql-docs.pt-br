---
description: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8ff8ab3db826d483f8f6df09277e1a5510aaf48
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98097706"
---
# <a name="sysdm_db_column_store_row_group_operational_stats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Retorna a atividade atual de e/s de nível de linha, de bloqueio e de método de acesso para RowGroups compactados em um índice columnstore. Use **Sys.dm_db_column_store_row_group_operational_stats** para controlar o período de tempo que uma consulta de usuário deve aguardar para ler ou gravar em um rowgroup compactado ou partição de um índice columnstore e identificar os grupos de itens que estão encontrando atividade de e/s significativa ou pontos de acesso.  
  
 Os índices columnstore na memória não aparecem nessa DMV.  
 
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela com o índice columnstore.|  
|**index_id**|**int**|ID do índice columnstore.|  
|**partition_number**|**int**|Número de partição com base 1 no índice ou heap.|  
|**row_group_id**|**int**|ID do rowgroup no índice columnstore. Isso é exclusivo em uma partição.|  
|**scan_count**|**int**|Número de verificações por meio do rowgroup desde a última reinicialização do SQL.|  
|**delete_buffer_scan_count**|**int**|Número de vezes que o buffer de exclusão foi usado para determinar as linhas excluídas nesse rowgroup. Isso inclui o acesso à tabela de hash na memória e ao árvore b subjacente.|  
|**index_scan_count**|**int**|Número de vezes que a partição de índice columnstore foi verificada. Isso é o mesmo para todos os grupos de rowgroup na partição.|  
|**rowgroup_lock_count**|**bigint**|Contagem cumulativa de solicitações de bloqueio para este rowgroup desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Número cumulativo de vezes que o mecanismo de banco de dados aguardou esse bloqueio de rowgroup desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Número cumulativo de milissegundos que o mecanismo de banco de dados aguardou nesse bloqueio de rowgroup desde a última reinicialização do SQL.|  
  
## <a name="permissions"></a>Permissões  
 Requer as seguintes permissões:  
  
-   Permissão CONTROL na tabela especificada por object_id.  
  
-   Permissão VIEW DATABASE STATE para retornar informações sobre todos os objetos no banco de dados, usando o curinga do objeto @*object_id* = NULL  
  
 Conceder VIEW DATABASE STATE permite que todos os objetos no banco de dados sejam retornados, independentemente de qualquer permissão CONTROL negada a objetos específicos.  
  
 Negar VIEW DATABASE STATE impede que todos os objetos do banco de dados sejam retornados, independentemente de qualquer permissão CONTROL concedida a objetos específicos. Além disso, quando o curinga do banco de dados @*database_id*= NULL é especificado, o banco de dados é omitido.  
  
 Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_db_index_usage_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_db_partition_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

