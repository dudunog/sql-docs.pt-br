---
description: sys.trace_columns (Transact-SQL)
title: sys.trace_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_columns
- trace_columns
- trace_columns_TSQL
- sys.trace_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_columns catalog view
ms.assetid: 5c48eb09-9e9b-45dd-b151-ca39b026ece5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 740f553e4809a5eb971bb7bfe7e97b5b628dfebd
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094378"
---
# <a name="systrace_columns-transact-sql"></a>sys.trace_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição de catálogo **Sys.trace_columns** contém uma lista de todas as colunas de evento de rastreamento. Essas colunas não são diferentes para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para obter uma lista completa de eventos de rastreamento com suporte, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_column_id**|**smallint**|ID exclusivo desta coluna.|  
|**name**|**nvarchar(128)**|Nome exclusivo desta coluna. Este parâmetro não é localizado.|  
|**type_name**|**nvarchar(128)**|Nome do tipo de dados desta coluna.|  
|**max_size**|**int**|Tamanho máximo dos dados desta coluna em bytes.|  
|**is_filterable**|**bit**|Indica se a coluna pode ser usada em uma especificação de filtro.<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeatable**|**bit**|Indica se a coluna pode ser referenciada nos dados de “coluna repetida”.<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeated_base**|**bit**|Indica se esta coluna é usada como uma chave exclusiva para referenciar dados repetidos.<br /><br /> 0 = false<br /><br /> 1 = true|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_categories ](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_events ](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_event_bindings ](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_subclass_values ](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
