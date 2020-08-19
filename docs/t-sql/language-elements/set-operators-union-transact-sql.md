---
description: Set Operators – UNION (Transact-SQL)
title: UNION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40bf24d7e1a5bcbc32307b5d5731907fb5f8463d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459308"
---
# <a name="set-operators---union-transact-sql"></a>Set Operators – UNION (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Concatena os resultados de duas consultas em um único conjunto de resultados. Você controla se o conjunto de resultados inclui linhas duplicadas:

- **UNION ALL** – inclui duplicatas.
- **UNION** – exclui duplicatas.

Uma operação **UNION** é diferente de uma **[JOIN](../queries/from-transact-sql.md)** :

- Uma **UNION** concatena conjuntos de resultados de duas consultas. Mas uma **UNION** não cria linhas individuais com base em colunas coletadas de duas tabelas.
- Uma **JOIN** compara colunas de duas tabelas para criar linhas de resultado compostas de colunas de duas tabelas.
  
A seguir são apresentadas as regras básicas de combinação dos conjuntos de resultados de duas consultas usando **UNION**:  
  
-   O número e a ordem das colunas devem ser iguais em todas as consultas.  
  
-   Os tipos de dados devem ser compatíveis.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
{ <query_specification> | ( <query_expression> ) }   
{ UNION [ ALL ]   
  { <query_specification> | ( <query_expression> ) } 
  [ ...n ] }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
\<query_specification> | (\<query_expression>) É uma especificação ou expressão de consulta que retorna dados a serem combinados com os dados de outra especificação ou expressão de consulta. As definições das colunas que fazem parte de uma operação UNION não precisam ser iguais, mas devem ser compatíveis por meio de conversão implícita. Quando os tipos de dados diferirem, o tipo de dados resultante será determinado com base nas regras de [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md). Quando os tipos são iguais mas diferem em precisão, escala ou extensão, o resultado se baseia nas mesmas regras para combinação de expressões. Para obter mais informações, confira [Precisão, escala e comprimento (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
As colunas do tipo de dados **xml** precisam ser iguais. Todas as colunas devem ter tipo para um esquema XML ou sem-tipo. Se tiverem tipo, elas deverão ter o tipo igual ao da coleção de esquema XML.  
  
UNION  
Especifica que vários conjuntos de resultados serão combinados e retornados como um único conjunto de resultados.  
  
ALL  
Incorpora todas as linhas nos resultados, incluindo duplicatas. Se não for especificado, as linhas duplicadas serão removidas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-simple-union"></a>a. Usando uma UNION simples  
No exemplo a seguir, o conjunto de resultados inclui o conteúdo das colunas `ProductModelID` e `Name` das tabelas `ProductModel` e `Gloves`.  
 
```sql
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>B. Usando SELECT INTO com UNION  
No exemplo a seguir, a cláusula `INTO` da segunda instrução `SELECT` especifica que a tabela denominada `ProductResults` mantém o conjunto de resultados final da união das colunas selecionadas das tabelas `ProductModel` e `Gloves`. A tabela `Gloves` é criada na primeira instrução `SELECT`.  
  
```sql
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. Usando UNION de duas instruções SELECT com ORDER BY  
A ordem de determinados parâmetros usados com a cláusula UNION é importante. O exemplo a seguir mostra o uso incorreto e correto de `UNION` em duas instruções `SELECT` nas quais uma coluna deve ser renomeada na saída.  
  
```sql
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. Usando UNION de três instruções SELECT para mostrar os efeitos de ALL e parênteses  
Os exemplos a seguir usam `UNION` para combinar os resultados de três tabelas que têm as mesmas 5 linhas de dados. O primeiro exemplo usa `UNION ALL` para mostrar os registros duplicados e retorna todas as 15 linhas. O segundo exemplo usa `UNION` sem `ALL` para eliminar as linhas duplicadas dos resultados combinados das três instruções `SELECT` e retorna 5 linhas.  
  
O terceiro exemplo usa `ALL` com a primeira `UNION` e parênteses cercam a segunda `UNION` que não está usando `ALL`. A segunda `UNION` é processada primeiro porque está entre parênteses e retorna 5 linhas porque a opção `ALL` não é usada e as duplicatas são removidas. Essas 5 linhas são combinadas com os resultados do primeiro `SELECT` usando as palavras-chave `UNION ALL`. Esse exemplo não remove as duplicatas entre os dois conjuntos de cinco linhas. O resultado final tem 10 linhas.  
  
```sql
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. Usando uma UNION simples  
No exemplo a seguir, o conjunto de resultados inclui o conteúdo das colunas `CustomerKey` das duas tabelas `FactInternetSales` e `DimCustomer`. Como a palavra-chave ALL não é usada, as duplicatas são excluídas dos resultados.  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. Usando UNION de duas instruções SELECT com ORDER BY  
 Quando qualquer instrução SELECT em uma instrução UNION incluir uma cláusula ORDER BY, essa cláusula deverá ser colocada após todas as instruções SELECT. O exemplo a seguir mostra o uso incorreto e correto de `UNION` em duas instruções `SELECT` nas quais uma coluna é ordenada com ORDER BY.  
  
```sql
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. Usando UNION de duas instruções SELECT com WHERE e ORDER BY  
O exemplo a seguir mostra o uso incorreto e correto de `UNION` em duas instruções `SELECT` nas quais WHERE e ORDER BY são necessários.  
  
```sql
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. Usando UNION de três instruções SELECT para mostrar os efeitos de ALL e de parênteses  
Os exemplos a seguir usam `UNION` para combinar os resultados da **mesma tabela** para demonstrar os efeitos de ALL e de parênteses ao usar `UNION`.  
  
O primeiro exemplo usa `UNION ALL` para mostrar registros duplicados e retorna cada linha na tabela de origem três vezes. O segundo exemplo usa `UNION` sem `ALL` para eliminar as linhas duplicadas dos resultados combinados das três instruções `SELECT` e retorna somente as linhas não duplicadas da tabela de origem.  
  
O terceiro exemplo usa `ALL` com a primeira `UNION` e parênteses delimitando a segunda `UNION` que não está usando `ALL`. A segunda `UNION` é processada primeiro porque está entre parênteses. Ela retorna somente as linhas não duplicadas da tabela porque a opção `ALL` não é usada e as duplicatas são removidas. Essas linhas são combinadas com os resultados da primeira `SELECT` usando as palavras-chave `UNION ALL`. Esse exemplo não remove as duplicatas entre os dois conjuntos.  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>Consulte Também  
[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
[Exemplos de SELECT (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md)  
