---
title: Cláusula OVER (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a cláusula OVER, que define um conjunto de linhas especificado pelo usuário em um conjunto de resultados da consulta.
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OVER_TSQL
- OVER
dev_langs:
- TSQL
helpviewer_keywords:
- order of rowsets [SQL Server]
- rowsets [SQL Server], windowing
- window function
- partitions [SQL Server], rowsets
- clauses [SQL Server], OVER
- rowsets [SQL Server], partitioning
- rowsets [SQL Server], ordering
- OVER clause
ms.assetid: ddcef3a6-0341-43e0-ae73-630484b7b398
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dd2c6c6f33f9a115196d9a2afc3ca700b3a4631
ms.sourcegitcommit: a81823f20262227454c0b5ce9c8ac607aaf537e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97684203"
---
# <a name="select---over-clause-transact-sql"></a>SELECT – Cláusula OVER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Determina o particionamento e a ordenação de um conjunto de linhas antes da aplicação da função de janela associada. Isto é, a cláusula OVER defines uma janela ou conjunto de linhas especificado pelo usuário em um conjunto de resultados de consulta. Uma função de janela computa um valor para cada linha na janela. Você pode usar a cláusula OVER com funções para computar valores agregados como médias móveis, agregações cumulativas, somas acumuladas ou os primeiros N resultados por grupo.  
  
-   [Funções de classificação](../../t-sql/functions/ranking-functions-transact-sql.md)  
  
-   [Funções de agregação](../../t-sql/functions/aggregate-functions-transact-sql.md)  
  
-   [Funções analíticas](../../t-sql/functions/analytic-functions-transact-sql.md)  
  
-   [Função NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md)  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server, Azure SQL Database, and Azure Synapse Analytics  
  
OVER (   
       [ <PARTITION BY clause> ]  
       [ <ORDER BY clause> ]   
       [ <ROW or RANGE clause> ]  
      )  
  
<PARTITION BY clause> ::=  
PARTITION BY value_expression , ... [ n ]  
  
<ORDER BY clause> ::=  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]  
  
<ROW or RANGE clause> ::=  
{ ROWS | RANGE } <window frame extent>  
  
<window frame extent> ::=   
{   <window frame preceding>  
  | <window frame between>  
}  
<window frame between> ::=   
  BETWEEN <window frame bound> AND <window frame bound>  
  
<window frame bound> ::=   
{   <window frame preceding>  
  | <window frame following>  
}  
  
<window frame preceding> ::=   
{  
    UNBOUNDED PRECEDING  
  | <unsigned_value_specification> PRECEDING  
  | CURRENT ROW  
}  
  
<window frame following> ::=   
{  
    UNBOUNDED FOLLOWING  
  | <unsigned_value_specification> FOLLOWING  
  | CURRENT ROW  
}  
  
<unsigned value specification> ::=   
{  <unsigned integer literal> }  
  
```  
  
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
OVER ( [ PARTITION BY value_expression ] [ order_by_clause ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

As funções da janela podem ter os seguintes argumentos na cláusula `OVER`:
- [PARTITION BY](#partition-by) divide o conjunto de resultados da consulta em partições.
- [ORDER BY](#order-by) define a ordem lógica das linhas dentro de cada partição do conjunto de resultados. 
- [ROWS/RANGE](#rows-or-range) limita as linhas dentro da partição com a especificação de pontos iniciais e finais na partição. Isso requer o argumento `ORDER BY`, e o valor padrão é do início da partição até o elemento atual se o argumento `ORDER BY` for especificado.

Se você não especificar nenhum argumento, as funções da janela serão aplicadas em todo o conjunto de resultados.
```sql
select 
      object_id
    , [min] = min(object_id) over()
    , [max] = max(object_id) over()
from sys.objects
```
 
|object_id | min | max |
|---|---|---|
| 3 | 3 | 2139154666 |
| 5 | 3 | 2139154666 |
| ... | ... | ... |
| 2123154609 |  3 | 2139154666 |
| 2139154666 |  3 | 2139154666 |

### <a name="partition-by"></a>PARTITION BY  
 Divide o conjunto de resultados da consulta em partições. A função de janela é aplicada separadamente a cada partição e a computação é reiniciada para cada partição.  

```sqlsyntax
PARTITION BY *value_expression* 
```
 
 Se PARTITION BY não for especificado, a função tratará todas as linhas da consulta como uma única partição.
A função será aplicada a todas as linhas da partição se você não especificar a cláusula `ORDER BY`.
  
#### <a name="partition-by-value_expression"></a>PARTITION BY *value_expression*  
 Especifica a coluna pela qual o conjunto de linhas é particionado. *value_expression* apenas pode se referir a colunas disponibilizadas pela cláusula FROM. *value_expression* não pode se referir a expressões ou aliases na lista de seleção. *value_expression* pode ser uma expressão de coluna, subconsulta escalar, função escalar ou variável definida pelo usuário. 
 
 ```sql
 select 
      object_id, type
    , [min] = min(object_id) over(partition by type)
    , [max] = max(object_id) over(partition by type)
from sys.objects
```

|object_id | type | min | max |
|---|---|---|---|
| 68195293  | PK    | 68195293  | 711673583 |
| 631673298 | PK    | 68195293  | 711673583 |
| 711673583 | PK    | 68195293  | 711673583 |
| ... | ... | ... |
| 3 | S | 3 | 98 |
| 5 | S |   3   | 98 |
| ... | ... | ... |
| 98    | S |   3   | 98 |
| ... | ... | ... |
  
### <a name="order-by"></a>ORDER BY  

```sqlsyntax
ORDER BY *order_by_expression* [COLLATE *collation_name*] [ASC|DESC]  
```

 Define a ordem lógica das linhas dentro de cada partição do conjunto de resultados. Ou seja, ela especificará a ordem lógica em que o cálculo da função da janela será executado. 
 - Caso não seja especificada, a ordem padrão será `ASC` e a função da janela usará todas as linhas na partição.
 - Se for especificada, e ROWS/RANGE não for especificada, o `RANGE UNBOUNDED PRECEDING AND CURRENT ROW` padrão será usado como padrão para o quadro de janela pelas funções que podem aceitar a especificação ROWS/RANGE opcional (por exemplo `min` ou `max`). 
 
```sql
select 
      object_id, type
    , [min] = min(object_id) over(partition by type order by object_id)
    , [max] = max(object_id) over(partition by type order by object_id)
from sys.objects
```

|object_id | type | min | max |
|---|---|---|---|
| 68195293  | PK    | 68195293  | 68195293 |
| 631673298 | PK    | 68195293  | 631673298 |
| 711673583 | PK    | 68195293  | 711673583 |
| ... | ... | ... |
| 3 | S | 3 | 3 |
| 5 | S |   3 | 5 |
| 6 | S |   3 | 6 |
| ... | ... | ... |
| 97    | S |   3 | 97 |
| 98    | S |   3 | 98 |
| ... | ... | ... |


 *order_by_expression*  
 Especifica uma coluna ou expressão na qual ordenar. *order_by_expression* apenas pode se referir a colunas disponibilizadas pela cláusula FROM. Um número inteiro não pode ser especificado para representar um nome de coluna ou alias.  
  
 COLLATE *collation_name*  
 Especifica que a operação ORDER BY deve ser executada de acordo com a ordenação especificada em *collation_name*. *collation_name* pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md). COLLATE é aplicável somente a colunas do tipo **char**, **varchar**, **nchar** e **nvarchar**.  
  
 **ASC** | DESC  
 Define que os valores na coluna especificada devem ser classificados em ordem crescente ou decrescente. ASC é a ordem de classificação padrão. Valores nulos são tratados como os menores valores possíveis.  
  
### <a name="rows-or-range"></a>LINHAS OU INTERVALO  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. 
  
 Limita mais as linhas dentro da partição com a especificação de pontos iniciais e finais na partição. Isso é feito pela especificação de um intervalo de linhas em relação à linha atual por associação lógica ou associação física. A associação física é obtida com o uso de uma cláusula ROWS.  
  
 A cláusula ROWS limita as linhas dentro de uma partição especificando um número fixo de linhas antes ou depois da linha atual. Alternativamente, a cláusula RANGE limita as linhas logicamente dentro de uma partição especificando um intervalo de valores em relação ao valor na linha atual. As linhas precedentes e seguintes são definidas com base na classificação na cláusula ORDER BY. O quadro de janela "RANGE ... CURRENT ROW…" inclui todas as linhas que têm os mesmos valores na expressão ORDER BY da linha atual. Por exemplo, ROWS BETWEEN 2 PRECEDING AND CURRENT ROW significa que a janela de linhas em que a função funciona tem três linhas de tamanho, iniciando com 2 linhas antes e incluindo a linha atual.  
 
```sql
select
      object_id
    , [preceding]   = count(*) over(order by object_id ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
    , [central] = count(*) over(order by object_id ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING )
    , [following]   = count(*) over(order by object_id ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
from sys.objects
order by object_id asc
```

|object_id | precedência | central | após |
|---|---|---|---|
| 3 | 1 | 3 | 156 |
| 5 | 2 | 4 | 155 |
| 6 | 3 | 5 | 154 |
| 7 | 4 | 5 | 153 |
| 8 | 5 | 5 | 152 |
| ...   | ...   | ...   | ... |
| 2112726579    | 153   | 5 | 4 |
| 2119678599    | 154   | 5 | 3 |
| 2123154609    | 155   | 4 | 2 |
| 2139154666    | 156   | 3 | 1 | 
  
> [!NOTE]  
>  ROWS ou RANGE requer que a cláusula ORDER BY seja especificada. Se ORDER BY contiver várias expressões de ordem, CURRENT ROW FOR RANGE considerará todas as colunas na lista ORDER BY ao determinar a linha atual.  
  
#### <a name="unbounded-preceding"></a>UNBOUNDED PRECEDING  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Especifica que a janela inicia na primeira linha da partição. UNBOUNDED PRECEDING só pode ser especificado como ponto de partida da janela.  
  
 \<unsigned value specification> PRECEDING  
 Especificado com \<unsigned value specification> para indicar o número de linhas ou valores que precederão a linha atual. Essa especificação não é permitida para RANGE.  
  
#### <a name="current-row"></a>CURRENT ROW  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. 
  
 Especifica que a janela inicia ou termina na linha atual quando usada com ROWS ou o valor atual quando usado com RANGE. CURRENT ROW pode ser especificado como um ponto de partida e ponto final.  
  
#### <a name="between-and"></a>BETWEEN AND  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. 
  
```sqlsyntax
BETWEEN <window frame bound > AND <window frame bound >  
```
 Usado com ROWS ou RANGE para especificar os pontos de limite inferiores (inicial) e superiores (finais) da janela. \<window frame bound> define o ponto de partida do limite e \<window frame bound> define o ponto de término do limite. O limite superior não pode ser menor que o limite inferior.  
  
#### <a name="unbounded-following"></a>UNBOUNDED FOLLOWING  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. 
  
 Especifica que a janela termina na última linha da partição. UNBOUNDED FOLLOWING só pode ser especificado como ponto de extremidade da janela. Por exemplo RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING define uma janela que inicia com a linha atual e termina com a última linha da partição.  
  
 \<unsigned value specification> FOLLOWING  
 Especificado com \<unsigned value specification> para indicar o número de linhas ou valores que sucede a linha atual. Quando \<unsigned value specification> FOLLOWING é especificado como o ponto de partida da janela, o ponto de término precisa ser \<unsigned value specification>FOLLOWING. Por exemplo, ROWS BETWEEN 2 FOLLOWING AND 10 FOLLOWING define uma janela que começa com a segunda linha após a linha atual e termina com a décima linha após a linha atual. Essa especificação não é permitida para RANGE.  
  
 Um literal de inteiro sem sinal  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 É um literal de inteiro positivo (inclusive 0) que especifica o número de linhas ou valores para inserir antes ou depois da linha ou valor atual. Essa especificação é válida somente para ROWS.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Mais de uma função de janela pode ser usado em uma única consulta com uma única cláusula FROM. A cláusula OVER para cada função pode ser diferente no particionamento e na ordenação.  
  
 Se PARTITION BY não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. 
 
### <a name="important"></a>Importante:

Se ROWS/RANGE for especificado e \<window frame preceding> for usado para \<window frame extent> (sintaxe curta), essa especificação será usada para o ponto de partida de limite de quadro de janela e CURRENT ROW será usado para o ponto de término do limite. Por exemplo "ROWS 5 PRECEDING" é igual a "ROWS BETWEEN 5 PRECEDING AND CURRENT ROW".  
  
> [!NOTE]
> Se ORDER BY não for especificado, toda a partição será usada para um quadro de janela. Isso só se aplica a funções que não requerem a cláusula ORDER BY. Se ROWS/RANGE não for especificado, mas ORDER BY for especificado, RANGE UNBOUNDED PRECEDING AND CURRENT ROW é usado como padrão para quadro de janela. Isso só se aplica a funções que podem aceitar a especificação de ROWS/RANGE opcional. Por exemplo, as funções de classificação não podem aceitar ROWS/RANGE, portanto, esse quadro de janela não é aplicado, mesmo que ORDER BY esteja presente e ROWS/RANGE não.  
    
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 A cláusula OVER não pode ser usada com a função de agregação CHECKSUM.  
  
 O RANGE não pode ser usado com \<unsigned value specification> PRECEDING ou \<unsigned value specification> FOLLOWING.  
  
 Dependendo da função de classificação, de agregação ou analítica usada com a cláusula OVER, talvez não haja suporte para \<ORDER BY clause> e/ou \<ROWS and RANGE clause>.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-over-clause-with-the-row_number-function"></a>a. Usando a cláusula OVER com a função ROW_NUMBER  
 O exemplo a seguir mostra como usar a cláusula OVER com a função ROW_NUMBER para exibir um número de linha para cada linha em uma partição. A cláusula ORDER BY especificada na cláusula OVER ordena as linhas em cada partição pela coluna `SalesYTD`. A cláusula ORDER BY na instrução SELECT determina a ordem na qual todo o conjunto de resultados da consulta é retornado.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ROW_NUMBER() OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS "Row Number",   
    p.LastName, s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0  
ORDER BY PostalCode;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Row Number      LastName                SalesYTD              PostalCode 
 --------------- ----------------------- --------------------- ---------- 
 1               Mitchell                4251368.5497          98027 
 2               Blythe                  3763178.1787          98027 
 3               Carson                  3189418.3662          98027 
 4               Reiter                  2315185.611           98027 
 5               Vargas                  1453719.4653          98027  
 6               Ansman-Wolfe            1352577.1325          98027  
 1               Pak                     4116871.2277          98055  
 2               Varkey Chudukatil       3121616.3202          98055  
 3               Saraiva                 2604540.7172          98055  
 4               Ito                     2458535.6169          98055  
 5               Valdez                  1827066.7118          98055  
 6               Mensa-Annan             1576562.1966          98055  
 7               Campbell                1573012.9383          98055  
 8               Tsoflias                1421810.9242          98055
 ```  
  
### <a name="b-using-the-over-clause-with-aggregate-functions"></a>B. Usando a cláusula OVER com funções de agregação  
 O exemplo a seguir usa a cláusula `OVER` com funções de agregação sobre todas as linhas retornadas pela consulta. Neste exemplo, o uso da cláusula `OVER` é mais eficiente que o uso de subconsultas para derivar os valores agregados.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,AVG(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Avg"  
    ,COUNT(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Count"  
    ,MIN(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Min"  
    ,MAX(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Max"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
SalesOrderID ProductID   OrderQty Total       Avg         Count       Min    Max  
------------ ----------- -------- ----------- ----------- ----------- ------ ------  
43659        776         1        26          2           12          1      6  
43659        777         3        26          2           12          1      6  
43659        778         1        26          2           12          1      6  
43659        771         1        26          2           12          1      6  
43659        772         1        26          2           12          1      6  
43659        773         2        26          2           12          1      6  
43659        774         1        26          2           12          1      6  
43659        714         3        26          2           12          1      6  
43659        716         1        26          2           12          1      6  
43659        709         6        26          2           12          1      6  
43659        712         2        26          2           12          1      6  
43659        711         4        26          2           12          1      6  
43664        772         1        14          1           8           1      4  
43664        775         4        14          1           8           1      4  
43664        714         1        14          1           8           1      4  
43664        716         1        14          1           8           1      4  
43664        777         2        14          1           8           1      4  
43664        771         3        14          1           8           1      4  
43664        773         1        14          1           8           1      4  
43664        778         1        14          1           8           1      4  
```  
  
 O exemplo a seguir mostra o uso da cláusula `OVER` com uma função de agregação em um valor calculado.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,CAST(1. * OrderQty / SUM(OrderQty) OVER(PARTITION BY SalesOrderID)   
        *100 AS DECIMAL(5,2))AS "Percent by ProductID"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Observe que as agregações são calculadas por `SalesOrderID` e o `Percent by ProductID` é calculado para cada linha de cada `SalesOrderID`.  
  
```  
SalesOrderID ProductID   OrderQty Total       Percent by ProductID  
------------ ----------- -------- ----------- ---------------------------------------  
43659        776         1        26          3.85  
43659        777         3        26          11.54  
43659        778         1        26          3.85  
43659        771         1        26          3.85  
43659        772         1        26          3.85  
43659        773         2        26          7.69  
43659        774         1        26          3.85  
43659        714         3        26          11.54  
43659        716         1        26          3.85  
43659        709         6        26          23.08  
43659        712         2        26          7.69  
43659        711         4        26          15.38  
43664        772         1        14          7.14  
43664        775         4        14          28.57  
43664        714         1        14          7.14  
43664        716         1        14          7.14  
43664        777         2        14          14.29  
43664        771         3        14          21.4  
43664        773         1        14          7.14  
43664        778         1        14          7.14  
  
 (20 row(s) affected)  
```  
  
### <a name="c-producing-a-moving-average-and-cumulative-total"></a>C. Gerando uma média móvel e o total cumulativo  
 O exemplo a seguir usa as funções AVG e SUM com a cláusula OVER para fornecer uma média móvel e um total cumulativo de vendas anuais para cada território na tabela `Sales.SalesPerson`. Os dados são particionados por `TerritoryID` e ordenados logicamente por `SalesYTD`. Isso significa que a função AVG é computada para cada território com base no ano de vendas. Observe que para `TerritoryID` 1, há duas linhas para o ano de vendas 2005 que representam os dois vendedores com vendas nesse ano. As vendas médias para essas duas linhas são computadas e a terceira linha que representa vendas do ano 2006 é incluída na computação.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(VARCHAR(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(VARCHAR(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(VARCHAR(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
 Neste exemplo, a cláusula OVER não inclui PARTITION BY. Isso significa que a função será aplicada a todas as linhas retornadas pela consulta. A cláusula ORDER BY especificada na cláusula OVER determina a ordem lógica na qual a função AVG é aplicada. A consulta retorna uma média móvel de vendas por ano para todos os territórios de vendas especificados na cláusula WHERE. A cláusula ORDER BY especificada na instrução SELECT determina a ordem na qual as linhas da consulta são exibidas.  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(VARCHAR(20),SalesYTD,1) AS SalesYTD  
   ,CONVERT(VARCHAR(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(VARCHAR(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
### <a name="d-specifying-the-rows-clause"></a>D. Especificando a cláusula ROWS  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 O exemplo a seguir usa a cláusula ROWS para definir uma janela na qual as linhas são computadas como a linha atual e o número *N* de linhas que seguem (linha 1 neste exemplo).  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(VARCHAR(20),SalesYTD,1) AS SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(VARCHAR(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        1,079,603.50  
287              NULL        519,905.93           2006        692,430.38  
285              NULL        172,524.45           2007        172,524.45  
283              1           1,573,012.94         2005        2,925,590.07  
280              1           1,352,577.13         2005        2,929,139.33  
284              1           1,576,562.20         2006        1,576,562.20  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        6,709,904.17  
281              4           2,458,535.62         2005        2,458,535.62  
```  
  
 No exemplo a seguir, a cláusula ROWS é especificada com UNBOUNDED PRECEDING. O resultado é que a janela inicia na primeira linha da partição.  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(VARCHAR(20),SalesYTD,1) AS SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(VARCHAR(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS UNBOUNDED PRECEDING),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        559,697.56  
287              NULL        519,905.93           2006        1,079,603.50  
285              NULL        172,524.45           2007        1,252,127.95  
283              1           1,573,012.94         2005        1,573,012.94  
280              1           1,352,577.13         2005        2,925,590.07  
284              1           1,576,562.20         2006        4,502,152.27  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        4,251,368.55  
281              4           2,458,535.62         2005        6,709,904.17  
  
```  
  
## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-the-over-clause-with-the-row_number-function"></a>E. Usando a cláusula OVER com a função ROW_NUMBER  
 O exemplo a seguir retorna o ROW_NUMBER para representantes de vendas com base em suas cotas de vendas atribuídas.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    FirstName, LastName,   
CONVERT(VARCHAR(13), SUM(SalesAmountQuota),1) AS SalesQuota   
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
 
### <a name="f-using-the-over-clause-with-aggregate-functions"></a>F. Usando a cláusula OVER com funções de agregação  
 Os exemplos a seguir mostram como usar a cláusula OVER com funções de agregação. Neste exemplo, o uso da cláusula OVER é mais eficiente do que o uso de subconsultas.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       AVG(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Avg,  
       COUNT(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Count,  
       MIN(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Min,  
       MAX(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Max  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 OrderNumber  Product  Qty  Total  Avg  Count  Min  Max  
 -----------  -------  ---  -----  ---  -----  ---  ---  
 SO43659      218      6    16     3    5      1    6  
 SO43659      220      4    16     3    5      1    6  
 SO43659      223      2    16     3    5      1    6  
 SO43659      229      3    16     3    5      1    6  
 SO43659      235      1    16     3    5      1    6  
 SO43664      229      1     2     1    2      1    1  
 SO43664      235      1     2     1    2      1    1  
 ```
 
 O exemplo a seguir mostra o uso da cláusula OVER com uma função de agregação em um valor calculado. Observe que as agregações são calculadas por `SalesOrderNumber` e o percentual da ordem de venda total é calculada para cada linha de cada `SalesOrderNumber`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey AS Product,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       CAST(1. * OrderQuantity / SUM(OrderQuantity)   
        OVER(PARTITION BY SalesOrderNumber)   
            *100 AS DECIMAL(5,2)) AS PctByProduct  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 A primeira inicialização desse conjunto de resultados é:  
  
 ```
 OrderNumber  Product  Qty  Total  PctByProduct  
 -----------  -------  ---  -----  ------------  
 SO43659      218      6    16     37.50  
 SO43659      220      4    16     25.00  
 SO43659      223      2    16     12.50  
 SO43659      229      2    16     18.75  
 ```
 
## <a name="see-also"></a>Consulte Também  
 [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [Funções analíticas &#40;Transact-SQL&#41;](../../t-sql/functions/analytic-functions-transact-sql.md)   
 [Excelente postagem no blog sobre funções de janela e OVER, em sqlmag.com, por Itzik Ben-Gan](https://www.itprotoday.com/sql-server/how-use-microsoft-sql-server-2012s-window-functions-part-1)  
  
  
