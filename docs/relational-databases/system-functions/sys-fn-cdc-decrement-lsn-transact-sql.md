---
description: sys.fn_cdc_decrement_lsn (Transact-SQL)
title: sys.fn_cdc_decrement_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_cdc_decrement_lsn
- sys.fn_cdc_decrement_lsn_TSQL
- sys.fn_cdc_decrement_lsn
- fn_cdc_decrement_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_decrement_lsn
- sys.fn_cdc_decrement_lsn
ms.assetid: 83c182ad-4713-439b-8769-9b7408aec8b4
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 460af637f6829940d3dce5282e2bab067a6b08c7
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093861"
---
# <a name="sysfn_cdc_decrement_lsn-transact-sql"></a>sys.fn_cdc_decrement_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o LSN (número de sequência de log) anterior na sequência baseada no LSN especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_decrement_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *lsn_value*  
 Valor do LSN. *lsn_value* é **binary (10)**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Comentários  
 O LSN retornado pela função é sempre inferior ao valor especificado e nenhum valor de LSN pode existir entre os dois valores.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `sys.fn_cdc_decrement_lsn` para definir o limite LSN superior em uma consulta que retorna linhas de dados alterados com valores LSN inferiores ao valor LSN máximo.  
  
```  
Use AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_decrement_lsn(sys.fn_cdc_get_max_lsn());  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all');   
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.fn_cdc_increment_lsn ](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.fn_cdc_get_min_lsn ](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.fn_cdc_get_max_lsn ](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
