---
description: sp_query_store_remove_query (Transact-SQL)
title: sp_query_store_remove_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SP_QUERY_STORE_REMOVE_QUERY
- SP_QUERY_STORE_REMOVE_QUERY_TSQL
- SYS.SP_QUERY_STORE_REMOVE_QUERY
- SYS.SP_QUERY_STORE_REMOVE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_remove_query
- sp_query_store_remove_query
ms.assetid: cc39ca92-3cba-478e-beef-65560aa84007
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4aff0b1ce7544474899793e7f1cc7344021cb157
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489149"
---
# <a name="sp_query_store_remove_query-transact-sql"></a>sp_query_store_remove_query (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Remove a consulta, bem como todos os planos associados e estatísticas de tempo de execução do repositório de consultas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_query_store_remove_query [ @query_id = ] query_id [;]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @query_id = ] query_id` É a ID da consulta a ser removida do repositório de consultas. *query_id* é um **bigint**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER** no banco de dados.
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as consultas no repositório de consultas.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 Depois de identificar o query_id que você deseja excluir, use o exemplo a seguir para excluir a consulta.  
  
 O exemplo a seguir.  
  
```  
EXEC sp_query_store_remove_query 3;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_query_store_force_plan ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_unforce_plan ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_reset_exec_stats ](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_flush_db ](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [Repositório de Consultas exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
