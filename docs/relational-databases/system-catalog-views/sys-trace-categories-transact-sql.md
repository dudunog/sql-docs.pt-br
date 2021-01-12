---
description: sys.trace_categories (Transact-SQL)
title: sys.trace_categories (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_categories
- trace_categories_TSQL
- sys.trace_categories
- sys.trace_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_categories catalog view
ms.assetid: f6a86766-e2a9-4d9f-a073-1b59e888ba7d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 3995de4afe010fd60d2176c8a6f3350ed8a94d95
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094403"
---
# <a name="systrace_categories-transact-sql"></a>sys.trace_categories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Classes de evento semelhantes são agrupadas por uma categoria. Cada linha na exibição de catálogo **Sys.trace_categories** identifica uma categoria que é exclusiva entre o servidor. Essas categorias não são diferentes para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para obter uma lista completa de eventos de rastreamento com suporte, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**category_id**|**smallint**|ID exclusiva dessa categoria. Essa coluna também está na exibição de catálogo **Sys.trace_events** .|  
|**name**|**nvarchar(128)**|Nome exclusivo dessa categoria. Este parâmetro não é localizado.|  
|**tipo**|**tinyint**|Tipo de categoria:<br /><br /> 0 = Normal<br /><br /> 1 = Conexão<br /><br /> 2 = Erro|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_columns ](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_events ](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_event_bindings ](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.trace_subclass_values ](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
