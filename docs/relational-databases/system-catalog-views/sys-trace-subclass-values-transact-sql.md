---
description: sys.trace_subclass_values (Transact-SQL)
title: sys.trace_subclass_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_subclass_values
- trace_subclass_values_TSQL
- sys.trace_subclass_values_TSQL
- trace_subclass_values
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_subclass_values catalog view
ms.assetid: 542b19ca-61c8-41ca-aa2e-0aba8906cc24
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8c39219bef217ba65797d9163a6b16ed6db15eff
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094341"
---
# <a name="systrace_subclass_values-transact-sql"></a>sys.trace_subclass_values (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição de catálogo **Sys.trace_subclass_values** contém uma lista de valores de coluna nomeados. Esses valores de subclasse não mudam para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para obter uma lista completa de eventos de rastreamento com suporte, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|ID do evento de rastreamento. Esse parâmetro também está na exibição de catálogo **Sys.trace_events** .|  
|**trace_column_id**|**smallint**|ID da coluna de rastreamento usado para enumeração. Esse parâmetro também está na exibição de catálogo **Sys.trace_columns** .|  
|**subclass_name**|**nvarchar(128)**|Significado do valor de coluna.|  
|**subclass_value**|**smallint**|Valor da coluna.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_categories ](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_columns ](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_events ](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_event_bindings ](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)  
  
  
