---
title: sys. fulltext_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9c139a45df1031ac47750d995780f8e13ea64f2c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133809"
---
# <a name="sysfulltext_index_columns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada coluna que faz parte de um índice de texto completo.    
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto do qual ela faz parte.|  
|**column_id**|**int**|ID da coluna que faz parte do índice de texto completo.|  
|**type_column_id**|**int**|ID da coluna de tipo que armazena a extensão de arquivo de documento fornecida pelo usuário-". doc", ". xls" e assim por diante-do documento em uma determinada linha. A coluna de tipo é especificada somente para colunas cujos dados exigem filtragem durante a indexação de texto completo. NULL se não for aplicável. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).|  
|**language_id**|**int**|O LCID do idioma cujo separador de palavras é usado para indexar esta coluna de texto completo.<br /><br /> 0 = Neutro.<br /><br /> Para obter mais informações, consulte [Sys. fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).|  
|**statistical_semantics**|**int**|1 = Esta coluna tem semânticas estatísticas habilitadas além da indexação de texto completo.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
