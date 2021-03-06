---
description: sp_prepare (Transact SQL)
title: sp_prepare (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9726ac52d0579c56de3c3ad971028cd606748726
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462677"
---
# <a name="sp_prepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

Prepara uma instrução parametrizada [!INCLUDE[tsql](../../includes/tsql-md.md)] e retorna um *identificador* de instrução para execução.  `sp_prepare` é invocado com a especificação de ID = 11 em um pacote do protocolo TDS.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>Argumentos  
 *processamento*  
 É um identificador de *identificador preparado* gerado pelo SQL Server. o *identificador* é um parâmetro necessário com um valor de retorno **int** .  
  
 *params*  
 Identifica instruções parametrizadas. A definição *params* das variáveis é substituída por marcadores de parâmetro na instrução. *params* é um parâmetro necessário que chama um valor de entrada **ntext**, **nchar** ou **nvarchar** . Insira um valor NULL se a instrução não for parametrizada.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O parâmetro *stmt* é necessário e chama um valor de entrada **ntext**, **nchar** ou **nvarchar** .  
  
 *options*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. *as opções* exigem o seguinte valor de entrada int:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>Exemplos  
a. O exemplo a seguir prepara e executa uma instrução simples.  
  
```sql  
DECLARE @P1 INT;  
EXEC sp_prepare @P1 OUTPUT,   
    N'@P1 NVARCHAR(128), @P2 NVARCHAR(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```

B. O exemplo a seguir prepara uma instrução no banco de dados AdventureWorks2016 e depois a executa usando o identificador.

```sql
-- Prepare query
DECLARE @P1 INT;  
EXEC sp_prepare @P1 OUTPUT,   
    N'@Param INT',  
    N'SELECT *
FROM Sales.SalesOrderDetail AS sod
INNER JOIN Production.Product AS p ON sod.ProductID = p.ProductID
WHERE SalesOrderID = @Param
ORDER BY Style DESC;';  

-- Return handle for calling application
SELECT @P1;
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
-----------
1

(1 row affected)
```

Em seguida, o aplicativo executa a consulta duas vezes usando o valor de identificador 1, antes de descartar o plano preparado.

```sql
EXEC sp_execute 1, 49879;  
GO

EXEC sp_execute 1, 48766;
GO

EXEC sp_unprepare 1; 
GO
```
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  

