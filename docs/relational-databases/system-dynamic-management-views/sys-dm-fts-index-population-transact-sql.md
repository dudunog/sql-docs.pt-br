---
description: sys.dm_fts_index_population (Transact-SQL)
title: sys.dm_fts_index_population (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bdcae6d4efe36e8b69ae2a211616178bba8af5f3
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323659"
---
# <a name="sysdm_fts_index_population-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre as populações de índice de texto completo e de frase-chave semântica que estão em andamento no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados que contém o índice de texto completo que está sendo populado.|  
|**catalog_id**|**int**|ID do catálogo de texto completo que contém este índice de texto completo.|  
|**table_id**|**int**|ID da tabela para a qual o índice de texto completo está sendo populado.|  
|**memory_address**|**varbinary (8)**|Endereço de memória da estrutura de dados interna que é usada para representar uma população ativa.|  
|**population_type**|**int**|Tipo de população. Um dos seguintes:<br /><br /> 1 = População completa<br /><br /> 2 = População incremental com base em carimbo de data/hora<br /><br /> 3 = Atualização manual de alterações controladas<br /><br /> 4 = Atualização em segundo plano de alterações controladas.|  
|**population_type_description**|**nvarchar(120)**|Descrição para o tipo de população.|  
|**is_clustered_index_scan**|**bit**|Indica se a população envolve uma verificação do índice clusterizado.|  
|**range_count**|**int**|Número de subintervalos nos quais esta população foi paralelizada.|  
|**completed_range_count**|**int**|Número de intervalos para os quais o processamento está concluído.|  
|**outstanding_batch_count**|**int**|Número atual de lotes pendentes para esta população. Para obter mais informações, consulte [sys.dm_fts_outstanding_batches &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md).|  
|**status**|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Status desta população. Observação: alguns dos estados são transitórios. Um dos seguintes:<br /><br /> 3 = Iniciando<br /><br /> 5 = Processando normalmente<br /><br /> 7 = Parou de processar<br /><br /> Por exemplo, esse status ocorre quando uma mesclagem automática estiver em andamento.<br /><br /> 11 = População anulada<br /><br /> 12 = processando uma extração de semelhança semântica|  
|**status_description**|**nvarchar(120)**|Descrição do status da população.|  
|**completion_type**|**int**|Status de como esta população foi concluída.|  
|**completion_type_description**|**nvarchar(120)**|Descrição do tipo de conclusão.|  
|**worker_count**|**int**|Esse valor é sempre 0.|  
|**queued_population_type**|**int**|Tipo da população, com base em alterações controladas, que seguirão a população atual, se houver.|  
|**queued_population_type_description**|**nvarchar(120)**|Descrição da população a ser seguida, se houver. Por exemplo, quando CHANGE TRACKING = AUTO e a população completa inicial estiver em andamento, essa coluna exibirá "População automática".|  
|**start_time**|**datetime**|Hora em que a população foi iniciada.|  
|**incremental_timestamp**|**timestamp**|Representa o carimbo de data/hora inicial para uma população completa. Para todos os outros tipos de população, esse valor é o último ponto de verificação confirmado que representa o andamento das populações.|  
  
## <a name="remarks"></a>Comentários  
 Quando a indexação semântica estatística está habilitada além da indexação de texto completo, a extração semântica e a população de frases-chave, além da extração de dados de semelhança de documento, ocorrem simultaneamente com a indexação de texto completo. A população do índice de semelhança de documento ocorre posteriormente, em uma segunda fase. Para obter mais informações, consulte [gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="physical-joins"></a>Junções físicas  
 ![Junções significativas dessa exibição de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "Junções significativas dessa exibição de gerenciamento dinâmico")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|Um para um|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|Um para um|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

