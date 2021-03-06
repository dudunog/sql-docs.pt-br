---
description: sys.trace_event_bindings (Transact-SQL)
title: sys.trace_event_bindings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_event_bindings_TSQL
- trace_event_bindings
- sys.trace_event_bindings
- trace_event_bindings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_event_bindings catalog view
ms.assetid: 22f534e1-4ed6-4b3e-9ead-1d1001a1b0f5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 709a6fdcf24036d5a8a26630902e8c7816478943
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094396"
---
# <a name="systrace_event_bindings-transact-sql"></a>sys.trace_event_bindings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição de catálogo **Sys.trace_event_bindings** contém uma lista de todas as combinações de uso possíveis de eventos e colunas. Para cada evento listado na coluna **trace_event_id** , todas as colunas disponíveis são listadas na coluna **trace_column_id** . Nem todas as colunas disponíveis são populadas toda vez que um determinado evento ocorre. Esses valores não mudam para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para obter uma lista completa de eventos de rastreamento com suporte, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|ID do evento de rastreamento. Essa coluna também está na exibição de catálogo **Sys.trace_events** .|  
|**trace_column_id**|**smallint**|ID da coluna de rastreamento. Essa coluna também está na exibição de catálogo **Sys.trace_columns** .|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_categories ](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_columns ](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_events ](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_subclass_values ](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
