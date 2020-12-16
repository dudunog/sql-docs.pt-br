---
title: ROW_NUMBER (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a função ROW_NUMBER. Essa função numera a saída de um conjunto de resultados.
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e53bb9ca4b2c3466a7dd694712e52d6c076306e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484168"
---
# <a name="row_number-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Numera a saída de um conjunto de resultados. Mais especificamente, retorna o número sequencial de uma linha em uma partição de um conjunto de resultados, começando em 1 na primeira linha de cada partição. 
  
`ROW_NUMBER` e `RANK` são semelhantes. `ROW_NUMBER` numera todas as linhas em sequência (por exemplo 1, 2, 3, 4, 5). `RANK` fornece o mesmo valor numérico para empates (por exemplo 1, 2, 2, 4, 5).   
  
> [!NOTE]
> `ROW_NUMBER` é um valor temporário calculado quando a consulta é executada. Para persistir números em uma tabela, consulte [Propriedade IDENTITY](../../t-sql/statements/create-table-transact-sql-identity-property.md) e [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md). 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 PARTITION BY *value_expression*  
 Divide o conjunto de resultados produzido pela cláusula [FROM](../../t-sql/queries/from-transact-sql.md) nas partições às quais a função ROW_NUMBER é aplicada. *value_expression* especifica a coluna pela qual o conjunto de resultados é particionado. Se `PARTITION BY` não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 A cláusula `ORDER BY` determina a sequência na qual as linhas recebem seu `ROW_NUMBER` exclusivo em uma partição especificada. É obrigatório. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint**  
  
## <a name="general-remarks"></a>Comentários gerais  
 Não há nenhuma garantia de que as linhas retornadas por uma consulta que usa `ROW_NUMBER()` serão ordenadas exatamente da mesma maneira com cada execução, a menos que as condições a seguir sejam verdadeiras.  
  
1.  Os valores da coluna particionada sejam exclusivos.  
  
2.  Os valores das `ORDER BY` colunas são exclusivos.  
  
3.  As combinações de valores da coluna de partição e colunas `ORDER BY` são exclusivas.  
  
 `ROW_NUMBER()` é não determinístico. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-examples"></a>a. Exemplos simples 

A consulta a seguir retorna as quatro tabelas do sistema em ordem alfabética.

```sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|name    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLES |
|modelo |FULL |
|msdb |SIMPLES |
|tempdb |SIMPLES |

Para adicionar uma coluna de número de linha na frente de cada linha, adicione uma coluna com a função `ROW_NUMBER`, nesse caso, chamada `Row#`. É necessário mover a cláusula `ORDER BY` até a cláusula `OVER`.

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLES |
|2 |modelo |FULL |
|3 |msdb |SIMPLES |
|4 |tempdb |SIMPLES |

A adição de uma cláusula `PARTITION BY` à coluna `recovery_model_desc` reiniciará a numeração quando o valor `recovery_model_desc` for alterado. 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |modelo |FULL |
|1 |master |SIMPLES |
|2 |msdb |SIMPLES |
|3 |tempdb |SIMPLES |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. Retornando o número de linha para vendedores  
 O exemplo a seguir calcula um número de linha para os vendedores da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] com base em sua classificação de vendas no ano até a data.  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. Retornando um subconjunto de linhas  
 O exemplo a seguir calcula números de linha para todas as linhas da tabela `SalesOrderHeader` na ordem de `OrderDate` e retorna somente as linhas de `50` a `60`.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-row_number-with-partition"></a>D. Usando ROW_NUMBER () com PARTITION  
 O exemplo a seguir usa o argumento `PARTITION BY` para particionar o conjunto de resultados da consulta pela coluna `TerritoryName`. A cláusula `ORDER BY` especificada na cláusula `OVER` ordena as linhas em cada partição pela coluna `SalesYTD`. A cláusula `ORDER BY` na instrução `SELECT` ordena o conjunto de resultados inteiro da consulta por `TerritoryName`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. Retornando o número de linha para vendedores  
 O exemplo a seguir retorna o `ROW_NUMBER` de representantes de vendas com base em suas cotas de vendas atribuídas.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
    FirstName, LastName,   
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 Este é um conjunto de resultados parcial.  

```  

RowNumber  FirstName  LastName            SalesQuota  
---------  ---------  ------------------  -------------  
1          Jillian    Carson              12,198,000.00  
2          Linda      Mitchell            11,786,000.00  
3          Michael    Blythe              11,162,000.00  
4          Jae        Pak                 10,514,000.00  
```

### <a name="f-using-row_number-with-partition"></a>F. Usando ROW_NUMBER () com PARTITION  
 O exemplo a seguir mostra o uso da função `ROW_NUMBER` com o argumento `PARTITION BY`. Isso faz com que a função `ROW_NUMBER` numere as linhas em cada partição.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 Este é um conjunto de resultados parcial.  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>Consulte Também  
 [RANK &#40;Transact-SQL&#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40;Transact-SQL&#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


