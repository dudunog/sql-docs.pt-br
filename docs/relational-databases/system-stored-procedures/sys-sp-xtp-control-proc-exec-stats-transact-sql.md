---
title: sys. sp_xtp_control_proc_exec_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9d011be97c90f156b8cd26cfb8fcc85963b75161
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442403"
---
# <a name="syssp_xtp_control_proc_exec_stats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Habilita a coleta de estatísticas para procedimentos armazenados compilados nativamente da instância.  
  
 Para habilitar a coleta de estatísticas no nível de consulta para procedimentos armazenados compilados nativamente, consulte [Sys. sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>Argumentos  
 @new_collection_value= *valor*  
 Determina se a coleta de estatísticas no nível do procedimento está ativada (1) ou desativada (0).  
  
 @new_collection_valueé definido como zero quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados é iniciado.  
  
 @old_collection_value= *valor*  
 Retorna o status atual.  
  
## <a name="return-code"></a>Código de retorno  
 0 para êxito. Diferente de zero para falha.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função sysadmin fixa.  
  
## <a name="code-samples"></a>Exemplos de Código  
 Para definir @new_collection_value e consultar o valor de@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
