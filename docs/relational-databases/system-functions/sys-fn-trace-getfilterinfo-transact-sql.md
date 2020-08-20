---
description: sys.fn_trace_getfilterinfo (Transact-SQL)
title: sys.fn_trace_getfilterinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
author: rothja
ms.author: jroth
ms.openlocfilehash: a76efe75df29423c1f788ace0f8dde8b158c6a0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454775"
---
# <a name="sysfn_trace_getfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os filtros aplicados a um rastreamento especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_id*  
 É a identificação do rastreamento. *trace_id* é **int**, sem padrão.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Retorna as informações a seguir. Para obter mais informações sobre as colunas, consulte [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|A identificação da coluna na qual o filtro é aplicado.|  
|**logical_operator**|**int**|Especifica se o operador AND ou OR é aplicado.|  
|**comparison_operator**|**int**|Especifica o tipo de comparação feita:<br /><br /> 0 = Igual<br /><br /> 1 = Diferente de<br /><br /> 2 = Maior que<br /><br /> 3 = Menor que<br /><br /> 4 = Maior que ou igual a<br /><br /> 5 = Menor que ou igual a<br /><br /> 6 = Like<br /><br /> 7 = Not like|  
|**value**|**sql_variant**|Especifica o valor no qual o filtro é aplicado.|  
  
## <a name="remarks"></a>Comentários  
 O usuário define *trace_id* valor para identificar, modificar e controlar o rastreamento. Quando passado a ID de um rastreamento específico, **fn_trace_getfilterinfo** retorna informações sobre qualquer filtro nesse rastreamento. Se o rastreamento especificado não tiver um filtro, essa função retornará um conjunto de linhas vazio. Quando é passada uma ID inválida, a função retorna um conjunto de linhas vazio. Para obter informações semelhantes sobre rastreamentos, consulte [Sys. fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre todos os filtros do rastreamento número 2.  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um rastreamento &#40;&#41;de Transact-SQL ](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setfilter ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_create ](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_generateevent ](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setstatus ](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys. fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
