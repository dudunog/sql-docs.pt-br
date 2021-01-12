---
description: sys.dm_os_memory_cache_counters (Transact-SQL)
title: sys.dm_os_memory_cache_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: b35568bdef71d81918a3c672682e1e6df1fb9da1
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092763"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna um instantâneo da integridade de um cache no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Sys.dm_os_memory_cache_counters** fornece informações de tempo de execução sobre as entradas de cache alocadas, seu uso e a fonte de memória para as entradas de cache.  
  
> **Observação:** Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_os_memory_cache_counters**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Indica o endereço (chave primária) dos contadores associados a um cache específico. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Especifica o nome do cache. Não permite valor nulo.|  
|**tipo**|**nvarchar(60)**|Indica o tipo de cache que é associado a esta entrada. Não permite valor nulo.|  
|**single_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de uma única página alocada. É a quantidade de memória alocada usando o alocador de uma única página. Faz referência a páginas de 8 KB usadas diretamente do pool de buffers para esse cache. Não permite valor nulo.|  
|**pages_kb**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Especifica o volume, em quilobytes, da memória alocada no cache. Não permite valor nulo.|  
|**multi_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de várias páginas alocadas. Esta é a quantidade de memória alocada usando o alocador de várias páginas do nó de memória. Esta memória é alocada fora do pool de buffers e se beneficia do alocador virtual dos nós de memória. Não permite valor nulo.|  
|**pages_in_use_kb**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Especifica o volume, em quilobytes, da memória que está alocada e em uso no cache. Permite valor nulo.  Os valores dos objetos do tipo `USERSTORE_<*>` não são rastreados.  NULL é relatado para eles.|  
|**single_pages_in_use_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de uma única página que está sendo usada. Permite valor nulo. Essas informações não são rastreadas para objetos do tipo USERSTORE_ \<*> e esses valores serão nulos.|  
|**multi_pages_in_use_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de várias páginas que está sendo usada. É NULLABLE. Essas informações não são rastreadas para objetos do tipo USERSTORE_ \<*> , e esses valores serão nulos.|  
|**entries_count**|**bigint**|Indica o número de entradas no número. Não permite valor nulo.|  
|**entries_in_use_count**|**bigint**|Indica o número de entradas no cache que está sendo usado. Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões 

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   

## <a name="see-also"></a>Consulte Também  
  [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


