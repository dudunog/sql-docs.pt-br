---
description: sys.column_store_segments (Transact-SQL)
title: sys. column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ebc2fe3ce3ddbdd02184e56d3629e8e6ccb0ce03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88379222"
---
# <a name="syscolumn_store_segments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Retorna uma linha para cada segmento de coluna em um índice columnstore. Há um segmento de coluna por coluna por rowgroup. Por exemplo, uma tabela com 10 RowGroups e 34 colunas retorna 340 linhas. 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
|**hobt_id**|**bigint**|A ID do heap ou o índice de árvore B (hobt) para a tabela que tem seu índice columnstore.|  
|**column_id**|**int**|ID da coluna columnstore.|  
|**segment_id**|**int**|ID do rowgroup. Para compatibilidade com versões anteriores, o nome da coluna continua sendo chamado segment_id embora seja a ID do rowgroup. Você pode identificar exclusivamente um segmento usando \<hobt_id, partition_id, column_id> , <segment_id>.|  
|**version**|**int**|Versão de formato do segmento de coluna.|  
|**encoding_type**|**int**|Tipo de codificação usado para esse segmento:<br /><br /> 1 = VALUE_BASED-não cadeia de caracteres/binário sem dicionário (muito semelhante a 4 com algumas variações internas)<br /><br /> 2 = VALUE_HASH_BASED-coluna não cadeia de caracteres/binária com valores comuns no dicionário<br /><br /> 3 = STRING_HASH_BASED-cadeia de caracteres/coluna binária com valores comuns no dicionário<br /><br /> 4 = STORE_BY_VALUE_BASED-não cadeia de caracteres/binário sem dicionário<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-cadeia de caracteres/binário sem dicionário<br /><br /> Todas as codificações aproveitam a codificação de bits e de tamanho de execução quando possível.|  
|**row_count**|**int**|Número de linhas no grupo de linhas.|  
|**has_nulls**|**int**|1 se o segmento de coluna tiver valores nulos.|  
|**base_id**|**bigint**|ID do valor de base se o tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não estiver sendo usado, base_id será definido como-1.|  
|**magnitude**|**float**|Magnitude se o tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não estiver sendo usado, a magnitude será definida como-1.|  
|**primary_dictionary_id**|**int**|Um valor de 0 representa o dicionário global. Um valor de-1 indica que não há nenhum dicionário global criado para esta coluna.|  
|**secondary_dictionary_id**|**int**|Um valor diferente de zero aponta para o dicionário local para esta coluna no segmento atual (ou seja, o rowgroup). Um valor de-1 indica que não há nenhum dicionário local para este segmento.|  
|**min_data_id**|**bigint**|Id de dados mínimo no segmento de coluna.|  
|**max_data_id**|**bigint**|Id de dados máximo no segmento de coluna.|  
|**null_value**|**bigint**|Valor usado para representar nulos.|  
|**on_disk_size**|**bigint**|Tamanho do segmento em bytes.|  
  
## <a name="remarks"></a>Comentários  
 A consulta a seguir retorna informações sobre segmentos de um índice columnstore.  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 Todas as colunas exigem pelo menos a permissão **View definition** na tabela. As colunas a seguir retornam NULL, a menos que o usuário também tenha a permissão **Select** : has_nulls, base_id, magnitude, min_data_id, max_data_id e null_value.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

