---
title: sys. pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 1b5e9e05e65a7121f30bfc0fc296229e943a8cd9
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197389"
---
# <a name="syspdw_nodes_columns-transact-sql"></a>sys. pdw_nodes_columns (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Mostra colunas para tabelas definidas pelo usuário e exibições definidas pelo usuário.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID do objeto ao qual esta coluna pertence.||  
|name|**sysname**|Nome da coluna. Exclusivo no objeto.||  
|column_id|**int**|ID da coluna. Exclusivo no objeto.||  
|system_type_id|**tinyint**|ID do tipo de sistema da coluna.||  
|user_type_id|**int**|ID do tipo da coluna, como definido pelo usuário.||  
|max_length|**smallint**|Comprimento máximo (em bytes) da coluna.|Inclui-1 (não é válido) para tipos de coluna sem suporte.|  
|precisão|**tinyint**|Precisão da coluna com base numérica, caso contrário é 0.||  
|scale|**tinyint**|Escala da coluna se numérica; caso contrário é 0.||  
|collation_name|**sysname**|Nome da ordenação da coluna, se for baseado em caracteres; caso contrário, será NULL.||  
|is_nullable|**bit**|1 = A coluna permite valor nulo.||  
|is_ansi_padded|**bit**|1 = A coluna usa o comportamento ANSI_PADDING ON se for de caractere, binária, ou variante.|Sempre 0.|  
|is_rowguidcol|**bit**|1 = A coluna é uma ROWGUIDCOL declarada.|Sempre 0.|  
|is_identity|**bit**|1 = A coluna tem valores de identidade.|Sempre 0.|  
|is_computed|**bit**|1 = A coluna é computada.|Sempre 0.|  
|is_filestream|**bit**|1 = A coluna é uma coluna de FILESTREAM.|Sempre 0.|  
|is_replicated|**bit**|1 = A coluna é replicada.|Sempre 0.|  
|is_non_sql_subscribed|**bit**|1 = a coluna tem um assinante não SQL.|Sempre 0.|  
|is_merge_published|**bit**|1 = A coluna é publicada por mesclagem.|Sempre 0.|  
|is_dts_replicated|**bit**|1 = a coluna é replicada usando o SSIS.|Sempre 0.|  
|is_xml_document|**bit**|1 = O conteúdo é um documento XML completo.|Sempre 0.|  
|xml_collection_id|**int**|0 = Nenhuma coleção de esquemas XML.|Sempre 0.|  
|default_object_id|**int**|ID do objeto padrão; 0 = nenhum padrão.|Sempre 0.|  
|rule_object_id|**int**|ID da regra autônoma associada à coluna. <br />0 = Nenhuma regra autônoma.|Sempre 0.|  
|is_sparse|**bit**|1 = A coluna é esparsa.|Sempre 0.|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas.|Sempre 0.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
