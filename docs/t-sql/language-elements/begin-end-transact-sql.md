---
title: BEGIN...END (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BEGIN
- BEGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e278e41fa2f27684b1ce249bb45b1dc78356753
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75325558"
---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Abrange uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para que um grupo de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] possa ser executado. BEGIN e END são palavras-chave da linguagem de controle de fluxo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>Argumentos  
 { *sql_statement* | *statement_block* }  
 É qualquer instrução ou agrupamento de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] válido, como definido com o uso de um bloco de instrução.  
  
## <a name="remarks"></a>Comentários  
 Os blocos BEGIN...END podem ser aninhados.  
  
 Embora todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] sejam válidas em um bloco BEGIN...END, certas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não devem ser agrupadas no mesmo lote ou bloco de instrução.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, `BEGIN` e `END` definem uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que são executadas em conjunto. Se o bloco `BEGIN...END` não tivesse sido incluído, ambas as instruções `ROLLBACK TRANSACTION` seriam executadas e as mensagens `PRINT` seriam retornadas.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 No exemplo a seguir, `BEGIN` e `END` definem uma série de instruções do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] que são executadas em conjunto. Se o bloco `BEGIN...END` não for incluído, o exemplo a seguir ficará em um loop contínuo.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
    SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Linguagem de controle de fluxo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  


