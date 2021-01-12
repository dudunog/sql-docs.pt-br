---
title: '[ ] Caractere curinga para correspondência de caracteres'
description: Use um caractere curinga para corresponder a um ou mais caracteres.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
author: cawrites
ms.author: chadam
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0cc55631431246f87a64c9a17fe953e34c454f3
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095870"
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \] (Curinga – caracteres para correspondência) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Encontra a correspondência de qualquer caractere único dentro do intervalo ou conjunto especificado entre colchetes `[ ]`. Esses caracteres curinga podem ser usados em comparações de cadeias de caracteres que envolvem a correspondência de padrões, como `LIKE` e `PATINDEX`.  

 
## <a name="examples"></a>Exemplos  
### <a name="a-simple-example"></a>A: Exemplo simples   
O exemplo a seguir retorna os nomes dos que começam com a letra `m`. `[n-z]` especifica que a segunda letra deve estar em algum lugar no intervalo de `n` a `z`. O caractere curinga `%` percentual permite caracteres ou nenhum caractere que começa com o caractere 3. Os bancos de dados `model` e `msdb` atendem a esse critério. O banco de dados `master` não atende ao critério e é excluído do conjunto de resultados.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 Você pode ter outros bancos de dados qualificados instalados.


### <a name="b-more-complex-example"></a>B: exemplo mais complexo   
 O exemplo a seguir usa o operador [] para encontrar as IDs e os nomes de todos os funcionários da [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] que possuem endereços com um código postal de quatro dígitos.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  

### <a name="c-using-a-set-that-combines-ranges-and-single-characters"></a>C: Usando um conjunto que combina intervalos e caracteres únicos

Um conjunto de curingas pode incluir caracteres únicos e intervalos. O exemplo a seguir usa o operador [] para localizar uma cadeia de caracteres que começa com um número ou uma série de caracteres especiais.

```sql
SELECT [object_id], OBJECT_NAME(object_id) AS [object_name], name, column_id 
FROM sys.columns 
WHERE name LIKE '[0-9!@#$.,;_]%';
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
object_id     object_name                         name  column_id
---------     -----------                         ----  ---------
615673241     vSalesPersonSalesByFiscalYears      2002  5
615673241     vSalesPersonSalesByFiscalYears      2003  6
615673241     vSalesPersonSalesByFiscalYears      2004  7
1591676718    JunkTable                           _xyz  1
```
  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40;Curinga – caracteres para correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; &#40;Curinga – caracteres para não correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_ &#40;Curinga – encontrar a correspondência de um caractere&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
