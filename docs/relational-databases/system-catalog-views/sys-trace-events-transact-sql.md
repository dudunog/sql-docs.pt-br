---
description: sys.trace_events (Transact-SQL)
title: sys.trace_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_events_TSQL
- trace_events
- sys.trace_events
- sys.trace_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_events catalog view
ms.assetid: e7d2c5df-0e17-4e94-9d41-d36c7ee60662
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 2a1d4bf30f4b59f9ccd8ff3bc04dccf8eb2a6d23
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094363"
---
# <a name="systrace_events-transact-sql"></a>sys.trace_events (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição de catálogo **Sys.trace_events** contém uma lista de todos os eventos de rastreamento do SQL. Esses eventos de rastreamento não são diferentes para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
 Para obter mais informações sobre esses eventos de rastreamento, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|ID exclusiva do evento. Essa coluna também está nas exibições de catálogo **Sys.trace_event_bindings** e **Sys.trace_subclass_values** .|  
|**category_id**|**smallint**|A ID de categoria do evento. Essa coluna também está na exibição de catálogo **Sys.trace_categories** .|  
|**name**|**nvarchar(128)**|Nome exclusivo deste evento. Este parâmetro não é localizado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Confira também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_categories ](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_columns ](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_event_bindings ](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_subclass_values ](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
