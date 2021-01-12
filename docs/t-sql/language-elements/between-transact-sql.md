---
description: BETWEEN (Transact-SQL)
title: BETWEEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
author: cawrites
ms.author: chadam
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d41c356b20dd0bb0577f10ee0abc47681ed38e7
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095993"
---
# <a name="between-transact-sql"></a>BETWEEN (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Especifica um intervalo a ser testado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *test_expression*  
 É a [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser testada no intervalo definido por *begin_expression* e *end_expression*. *test_expression* precisa ser do mesmo tipo de dados que *begin_expression* e *end_expression*.  
  
 NOT  
 Especifica que o resultado do predicado deve ser negado.  
  
 *begin_expression*  
 É qualquer expressão válida. *begin_expression* precisa ser do mesmo tipo de dados que *test_expression* e *end_expression*.  
  
 *end_expression*  
 É qualquer expressão válida. *end_expression* precisa ser do mesmo tipo de dados que *test_expression* e *begin_expression*.  
  
 AND  
 Atua como um espaço reservado que indica se *test_expression* deve estar dentro do intervalo indicado por *begin_expression* e *end_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 BETWEEN retornará **TRUE** se o valor de *test_expression* for maior ou igual ao valor de *begin_expression* e menor ou igual ao valor de *end_expression*.  
  
 NOT BETWEEN retornará **TRUE** se o valor de *test_expression* for menor que o valor de *begin_expression* ou maior que o valor de *end_expression*.  
  
## <a name="remarks"></a>Comentários  
 Para especificar um intervalo exclusivo, use os operadores maior que (>) e menor que (<). Se qualquer entrada para o predicado BETWEEN ou NOT BETWEEN for NULL, o resultado será UNKNOWN.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-between"></a>a. Usando BETWEEN  
 O exemplo a seguir retorna informações sobre as funções de banco de dados em um banco de dados. A primeira consulta retorna todas as funções. O segundo exemplo usa a cláusula `BETWEEN` para limitar as funções aos valores `database_id` especificados.  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. Como usar > e < em vez de BETWEEN  
 O exemplo a seguir usa os operadores maior que (`>`) e menor que (`<`) e, como esses operadores não são inclusivos, retorna nove linhas em vez das dez retornadas no exemplo anterior.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. Usando NOT BETWEEN  
 O exemplo a seguir localiza todas as linhas fora de um intervalo especificado de `27` a `30`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. Usando BETWEEN com valores de data e hora  
 O exemplo a seguir recupera as linhas nas quais os valores de **datetime** estão entre `'20011212'` e `'20020105'`, inclusivo.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 A consulta recupera as linhas esperadas porque os valores de data na consulta e os valores de **datetime** armazenados na coluna `RateChangeDate` foram especificados sem a parte de hora da data. Quando a parte de hora não é especificada, o padrão é 12:00. Observe que uma linha que contém uma parte de hora posterior a 00h00 em 2002-01-05 não será retornada por essa consulta porque está fora do intervalo.  
  
  
## <a name="see-also"></a>Consulte Também  
 [&#62; &#40;Maior que&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60; &#40;Menor que&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


