---
description: SET STATISTICS TIME (Transact-SQL)
title: SET STATISTICS TIME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 36db16f45f3f73742c89b6269fedc5c4603e648f
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096889"
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Exibe o número de milissegundos necessários para analisar, compilar e executar cada instrução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
SET STATISTICS TIME { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
 Quando SET STATISTICS TIME for ON, serão exibidas as estatísticas de hora da instrução. Se OFF, as estatísticas de hora não serão exibidas.  
  
 A configuração de SET STATISTICS TIME é definida no momento da execução ou do tempo de execução, e não no momento da análise.  
  
 O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode fornecer estatísticas precisas em modo fibra, que é ativado quando a opção de configuração **lightweight pooling** é habilitada.  
  
 A coluna **cpu** na tabela **sysprocesses** apenas é atualizada quando uma consulta é executada com SET STATISTICS TIME ON. Quando SET STATISTICS TIME for OFF, será retornado **0**.  
  
 As configurações ON e OFF também afetam a coluna de CPU na Exibição de Informações de Processos da Atividade Atual no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Para usar SET STATISTICS TIME, os usuários devem ter as permissões apropriadas para executar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. A permissão SHOWPLAN não é exigida.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo mostra os tempos de execução, análise e compilação do servidor.  
  
```sql
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
