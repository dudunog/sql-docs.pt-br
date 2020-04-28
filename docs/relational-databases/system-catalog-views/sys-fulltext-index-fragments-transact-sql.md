---
title: sys. fulltext_index_fragments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 295d924422410bbf247d9b96d27b705fdfe3b5d3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133815"
---
# <a name="sysfulltext_index_fragments-transact-sql"></a>sys.fulltext_index_fragments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Um índice FULLTEXT usa tabelas internas chamadas de *fragmentos de índice de texto completo* para armazenar os dados de índice invertidos. Esta exibição pode ser usada para consultar os metadados sobre estes fragmentos. Esta exibição contém uma linha para cada fragmento de índice de texto completo em toda tabela que contém um índice de texto completo.  
 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|table_id|**int**|ID de objeto da tabela que contém o fragmento do índice de texto completo.|  
|fragment_object_id|**int**|ID de objeto da tabela interna associado com o fragmento.|  
|fragment_id|**int**|ID lógico do fragmento de índice de texto completo. Ele é exclusivo em todos os fragmentos para esta tabela.|  
|timestamp|**timestamp**|Timestamp associado com a criação do fragmento. O timestamps dos fragmentos mais recentes são maiores do que o timestamps de fragmentos mais antigos.|  
|data_size|**int**|Tamanho lógico do fragmento em bytes.|  
|row_count|**int**|Número de linhas individuais no fragmento.|  
|status|**int**|Status do fragmento, um de:<br /><br /> 0 = Criado recentemente e não utilizado ainda<br /><br /> 1 = Sendo usado para inserção durante população ou mesclagem de índice de texto completo<br /><br /> 4 = Fechado. Pronto para consulta<br /><br /> 6 = Sendo usado para entrada de mesclagem e pronto para consulta<br /><br /> 8 = Marcado para exclusão. Não será usado para consulta e mesclagem de origem.<br /><br /> Um status de 4 ou 6 significa que o fragmento faz parte do índice de texto completo lógico e pode ser consultado; ou seja, é um fragmento *passível* de consulta.|  
  
## <a name="remarks"></a>Comentários  
 A exibição do catálogo sys.fulltext_index_fragments pode ser usada para consultar o número de fragmentos que formam um índice de texto completo. Se estiver observando um baixo desempenho de consulta de texto completo, é possível usar sys.fulltext_index_fragments para consultar o número de fragmentos que podem ser consultados (status = 4 ou 6) no índice de texto completo desta forma:   
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 Se existirem diversos fragmentos que podem ser consultados, a Microsoft recomenda que você reorganize o catálogo de texto completo que contém um índice de texto completo para mesclar os fragmentos juntos. Para reorganizar um catálogo de texto completo, use [ALTER FULLTEXT catálogo](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* reorganizar. Por exemplo, para reorganizar um catálogo de texto completo chamado banco de dados `ftCatalog` in the `AdventureWorks2012`, digite:  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
