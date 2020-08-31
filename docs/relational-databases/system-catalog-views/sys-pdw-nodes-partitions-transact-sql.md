---
description: sys. pdw_nodes_partitions (Transact-SQL)
title: sys. pdw_nodes_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 82903661be207c73b1b848e8273b594ff49d1642
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062265"
---
# <a name="syspdw_nodes_partitions-transact-sql"></a>sys. pdw_nodes_partitions (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém uma linha para cada partição de todas as tabelas e a maioria dos tipos de índices em um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] banco de dados. Todas as tabelas e índices contêm pelo menos uma partição, independentemente de estarem ou não particionados explicitamente.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|ID da partição. É exclusivo em um banco de dados.|  
|object_id|**int**|ID do objeto ao qual pertence o particionamento. Toda tabela ou exibição é composta por pelo menos uma partição.|  
|index_id|**int**|Identificação do objeto ao qual pertence o particionamento.|  
|partition_number|**int**|Número de partição com base em um 1 no índice ou heap de propriedade. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] , o valor dessa coluna é 1.|  
|hobt_id|**bigint**|ID da heap ou árvore B de dados (HoBT) que contém as linhas desta partição.|  
|rows|**bigint**|Número aproximado de linhas nesta partição. |  
|data_compression|**int**|Indica o estado da compactação de cada partição:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|**nvarchar(60)**|Indica o estado da compactação de cada partição. Os valores possíveis são NONE, ROW e PAGE.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>Exemplo A: exibir linhas em cada partição dentro de cada distribuição 

**Aplica-se a:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
Para exibir o número de linhas em cada partição em cada distribuição, use [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) .

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>Exemplo B: usa exibições do sistema para exibir linhas em cada partição de cada distribuição de uma tabela

**Aplica-se a:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
Essa consulta retorna o número de linhas em cada partição de cada distribuição da tabela `myTable` .  
 
```sql  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

