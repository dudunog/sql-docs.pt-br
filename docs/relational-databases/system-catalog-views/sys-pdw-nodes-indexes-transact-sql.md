---
description: sys. pdw_nodes_indexes (Transact-SQL)
title: sys. pdw_nodes_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f6c518d53122015af3e86350b0037e1b88604543
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490239"
---
# <a name="syspdw_nodes_indexes-transact-sql"></a>sys. pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Retorna índices para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID do objeto ao qual este índice pertence.||  
|name|**sysname**|Nome do índice. O nome é exclusivo somente dentro do objeto. NULL = Heap||  
|index_id|**int**|ID do índice. index_id só é exclusivo dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> >1 = Índice não clusterizado||  
|type|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = Não clusterizado<br /><br /> 5 = índice columnstore com otimização de memória xVelocity clusterizado|  
|type_desc|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> COLUMNSTORE CLUSTERIZADO||  
|is_unique|**bit**|0 = O índice não é exclusivo.|Sempre 0.|  
|data_space_id|**int**|ID do espaço de dados para este índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = object_id é uma função com valor de tabela.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY está OFF.|Sempre 0.|  
|is_primary_key|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.|Sempre 0.|  
|is_unique_constraint|**bit**|1 = O índice faz parte de uma restrição UNIQUE.|Sempre 0.|  
|fill_factor|**tinyint**|> 0 = porcentagem FILLFACTOR usada quando o índice foi criado ou recriado.<br /><br /> 0 = Valor padrão|Sempre 0.|  
|is_padded|**bit**|0 = PADINDEX está OFF.|Sempre 0.|  
|is_disabled|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.||  
|is_hypothetical|**bit**|0 = O índice não é hipotético.|Sempre 0.|  
|allow_row_locks|**bit**|1 = O índice permite bloqueios de linha.|Sempre 1.|  
|allow_page_locks|**bit**|1 = O índice permite bloqueios de página.|Sempre 1.|  
|has_filter|**bit**|0 = O índice não tem um filtro.|Sempre 0.|  
|filter_definition|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.|Sempre nulo.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
