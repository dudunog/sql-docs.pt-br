---
title: SET ARITHIGNORE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ARITHIGNORE
- SET_ARITHIGNORE_TSQL
- ARITHIGNORE
- ARITHIGNORE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ARITHIGNORE statement
- overflow errors [SQL Server]
- ARITHIGNORE option
- divide-by-zero errors
ms.assetid: 71b2c2a5-c83a-4dfe-8469-237987a6e503
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 75571e6db8b13c91f119ef233735e98132ed845d
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634407"
---
# <a name="set-arithignore-transact-sql"></a>SET ARITHIGNORE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Controla se são retornadas mensagens de erro de estouro ou erros de divisão por zero durante uma consulta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database

SET ARITHIGNORE { ON | OFF }
```

```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

SET ARITHIGNORE OFF
```

## <a name="remarks"></a>Comentários  
 A configuração SET ARITHIGNORE apenas controla se uma mensagem de erro é retornada. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um NULL em um cálculo que envolve um erro de estouro ou divisão por zero, independentemente dessa configuração. A configuração SET ARITHABORT pode ser usada para determinar se a consulta foi terminada. Essa configuração não afeta erros que ocorrem durante instruções INSERT, UPDATE e DELETE.  
  
 Se SET ARITHABORT ou SET ARITHIGNORE estiver definida como OFF e SET ANSI_WARNINGS como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda retornará uma mensagem de erro quando encontrar erros de divisão por zero ou de estouro.  
  
 A configuração de SET ARITHIGNORE é definida no momento da execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @ARITHIGNORE VARCHAR(3) = 'OFF';  
IF ( (128 & @@OPTIONS) = 128 ) SET @ARITHIGNORE = 'ON';  
SELECT @ARITHIGNORE AS ARITHIGNORE;  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso das duas configurações de `SET ARITHIGNORE` com os dois tipos de erros de consulta.  
  
```  
SET ARITHABORT OFF;  
SET ANSI_WARNINGS OFF  
GO  
  
PRINT 'Setting ARITHIGNORE ON';  
GO  
-- SET ARITHIGNORE ON and testing.  
SET ARITHIGNORE ON;  
GO  
SELECT 1 / 0 AS DivideByZero;  
GO  
SELECT CAST(256 AS TINYINT) AS Overflow;  
GO  
  
PRINT 'Setting ARITHIGNORE OFF';  
GO  
-- SET ARITHIGNORE OFF and testing.  
SET ARITHIGNORE OFF;  
GO  
SELECT 1 / 0 AS DivideByZero;  
GO  
SELECT CAST(256 AS TINYINT) AS Overflow;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir demonstra os erros de divisão por zero e de estouro. Esse exemplo não retorna uma mensagem de erro para esses erros porque ARITHIGNORE é OFF.  
  
```  
-- SET ARITHIGNORE OFF and testing.  
SET ARITHIGNORE OFF;  
SELECT 1 / 0 AS DivideByZero;  
SELECT CAST(256 AS TINYINT) AS Overflow;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)  
  
  

