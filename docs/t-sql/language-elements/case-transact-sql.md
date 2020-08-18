---
title: CASE (Transact-SQL)
description: Referência de Transact-SQL para a expressão CASE. CASE avalia uma lista de condições para retornar resultados específicos.
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CASE_TSQL
- CASE
dev_langs:
- TSQL
helpviewer_keywords:
- CASE expression [Transact-SQL]
- simple CASE expression
- comparing expressions
- searched CASE expression
ms.assetid: 658039ec-8dc2-4251-bc82-30ea23708cee
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0091a060bc75b87ef40d03a48c25b5154c00ee4
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88200429"
---
# <a name="case-transact-sql"></a>CASE (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Avalia uma lista de condições e retorna uma das várias expressões de resultado possíveis.  
  
 A expressão CASE tem dois formatos:  
  
-   A expressão CASE simples compara uma expressão com um conjunto de expressões simples para determinar o resultado.  
  
-   A expressão CASE pesquisada avalia um conjunto de expressões boolianas para determinar o resultado.  
  
 Os dois formatos dão suporte a um argumento ELSE opcional.  
  
 CASE pode ser usada em qualquer instrução ou cláusula que permita uma expressão válida. Por exemplo, você pode usar CASE em instruções, como SELECT, UPDATE, DELETE e SET, e em cláusulas, como select_list, IN, WHERE, ORDER BY e HAVING.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
Simple CASE expression:   
CASE input_expression   
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END   
Searched CASE expression:  
CASE  
     WHEN Boolean_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CASE  
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos  
 *input_expression*  
 É a expressão avaliada quando o formato CASE simples é usado. *input_expression* é qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
 WHEN *when_expression*  
 É uma expressão simples com a qual *input_expression* é comparada quando o formato CASE simples é usado. *when_expression* é qualquer expressão válida. Os tipos de dados de *input_expression* e cada *when_expression* devem ser os mesmos ou devem ser uma conversão implícita.  
  
 THEN *result_expression*  
 É a expressão retornada quando *input_expression* igual a *when_expression* é avaliada como TRUE ou *Boolean_expression* é avaliada como TRUE. *result expression* é qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
 ELSE *else_result_expression*  
 É a expressão retornada se nenhuma operação de comparação for avaliada como TRUE. Se esse argumento for omitido e nenhuma operação de comparação for avaliada como TRUE, CASE retornará NULL. *else_result_expression* é qualquer expressão válida. Os tipos de dados de *else_result_expression* e qualquer *result_expression* devem ser os mesmos ou devem ser uma conversão implícita.  
  
 WHEN *Boolean_expression*  
 É a expressão booliana avaliada quando o formato CASE simples é usado. *Boolean_expression* é qualquer expressão booliana válida.  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Retorna o tipo de precedência mais alto do conjunto de tipos em *result_expressions* e a *else_result_expression* opcional. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
### <a name="return-values"></a>Valores de retorno  
 **Expressão CASE simples:**  
  
 A expressão CASE simples opera comparando a primeira expressão com a expressão em cada cláusula WHEN por equivalência. Se essas expressões forem equivalentes, a expressão na cláusula THEN será retornada.  
  
-   Permite somente uma verificação de igualdade.  
  
-   Na ordem especificada, avalia input_expression = when_expression para cada cláusula WHEN.  
  
-   Retorna a *result_expression* da primeira *input_expression* = *when_expression* que é avaliada como TRUE.  
  
-   Se nenhuma *input_expression* = *when_expression* for avaliada como TRUE, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará a *else_result_expression*, caso uma cláusula ELSE tenha sido especificada, ou um valor NULL, caso nenhuma cláusula ELSE tenha sido especificada.  
  
 **Expressão CASE pesquisada:**  
  
-   Avalia, na ordem especificada, a *Boolean_expression* de cada cláusula WHEN.  
  
-   Retorna *result_expression* da primeira *Boolean_expression* que é avaliada como TRUE.  
  
-   Se nenhuma *Boolean_expression* for avaliada como TRUE, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará a *else_result_expression*, caso uma cláusula ELSE tenha sido especificada, ou um valor NULL, caso nenhuma cláusula ELSE tenha sido especificada.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite apenas 10 níveis de aninhamento em expressões CASE.  
  
 A expressão CASE não pode ser usada para controlar o fluxo de execução de instruções Transact-SQL, blocos de instruções, funções definidas pelo usuário e procedimentos armazenados. Para obter uma lista dos métodos de controle de fluxo, consulte [Linguagem de controle de fluxo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md).  
  
 A expressão CASE avalia suas condições em sequência e para com a primeira condição satisfatória. Em algumas situações, uma expressão é avaliada antes de uma expressão CASE receber os resultados da expressão como sua entrada. É possível que haja erros na avaliação dessas expressões. As expressões agregadas que aparecem em argumentos WHEN de uma expressão CASE são avaliadas primeiro e, em seguida, são fornecidas para a expressão CASE. Por exemplo, a seguinte consulta gera um erro de divisão por zero ao gerar o valor da agregação MAX. Isso ocorre antes da avaliação da expressão CASE.  
  
```sql  
WITH Data (value) AS   
(   
SELECT 0   
UNION ALL   
SELECT 1   
)   
SELECT   
   CASE   
      WHEN MIN(value) <= 0 THEN 0   
      WHEN MAX(1/value) >= 100 THEN 1   
   END   
FROM Data ;  
```  
  
 Você deve depender somente da ordem de avaliação das condições WHEN para expressões escalares (incluindo subconsultas não correlacionadas que retornam escalares), e não para expressões agregadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-select-statement-with-a-simple-case-expression"></a>a. Usando uma instrução SELECT com uma expressão CASE simples  
 Dentro de uma instrução `SELECT`, uma expressão `CASE` simples é permitida somente para uma verificação de igualdade; nenhuma outra comparação é feita. O exemplo a seguir usa a expressão `CASE` para alterar a exibição de categorias de linhas de produto para torná-las mais compreensíveis.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   Name  
FROM Production.Product  
ORDER BY ProductNumber;  
GO  
  
```  
  
### <a name="b-using-a-select-statement-with-a-searched-case-expression"></a>B. Usando uma instrução SELECT com uma expressão CASE pesquisada  
 Dentro de uma instrução `SELECT`, a expressão `CASE` pesquisada é permitida para valores a serem substituídos no conjunto de resultados com base nos valores de comparação. O exemplo a seguir exibe o preço da lista como um comentário de texto com base na faixa de preços de um produto.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Name, "Price Range" =   
      CASE   
         WHEN ListPrice =  0 THEN 'Mfg item - not for resale'  
         WHEN ListPrice < 50 THEN 'Under $50'  
         WHEN ListPrice >= 50 and ListPrice < 250 THEN 'Under $250'  
         WHEN ListPrice >= 250 and ListPrice < 1000 THEN 'Under $1000'  
         ELSE 'Over $1000'  
      END  
FROM Production.Product  
ORDER BY ProductNumber ;  
GO  
  
```  
  
### <a name="c-using-case-in-an-order-by-clause"></a>C. Usando CASE em uma cláusula ORDER BY  
 O exemplo a seguir usa a expressão CASE em uma cláusula ORDER BY para determinar a ordem de classificação das linhas com base no valor da coluna fornecido. No primeiro exemplo, é avaliado o valor da coluna `SalariedFlag` da tabela `HumanResources.Employee`. Funcionários que têm o `SalariedFlag` definido como 1 são retornados pelo `BusinessEntityID` em ordem decrescente. Funcionários que têm o `SalariedFlag` definido como 0 são retornados pelo `BusinessEntityID` em ordem crescente. No segundo exemplo, o conjunto de resultados será ordenado pela coluna `TerritoryName` quando a coluna `CountryRegionName` for igual a 'United States' e por `CountryRegionName` para todas as outras linhas.  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
### <a name="d-using-case-in-an-update-statement"></a>D. Usando CASE em uma instrução UPDATE  
 O exemplo a seguir usa a expressão CASE em uma instrução UPDATE para determinar o valor definido para a coluna `VacationHours` para funcionários com `SalariedFlag` definido como 0. Ao subtrair 10 horas dos resultados de `VacationHours` em um valor negativo, `VacationHours` é aumentado em 40 horas; caso contrário, `VacationHours` é aumentado em 20 horas. A cláusula OUTPUT é usada para exibir os valores de antes e depois das férias.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)  
       END  
    )  
OUTPUT Deleted.BusinessEntityID, Deleted.VacationHours AS BeforeValue,   
       Inserted.VacationHours AS AfterValue  
WHERE SalariedFlag = 0;  
  
```  
  
### <a name="e-using-case-in-a-set-statement"></a>E. Usando CASE em uma instrução SET  
 O exemplo a seguir usa a expressão CASE em uma instrução SET na função com valor de tabela `dbo.GetContactInfo`. No banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], todo os dados relacionados com pessoas são armazenados na tabela `Person.Person`. Por exemplo, a pessoa pode ser um funcionário, um representante de fornecedor ou um cliente. A função retorna o nome e o sobrenome de determinado `BusinessEntityID` e o tipo de contato dessa pessoa. A expressão CASE na instrução SET determina o valor a ser exibido para a coluna `ContactType` com base na existência da coluna `BusinessEntityID` nas tabelas `Employee`, `Vendor` ou `Customer`.  
  
```  
  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.GetContactInformation(@BusinessEntityID int)  
    RETURNS @retContactInformation TABLE   
(  
BusinessEntityID int NOT NULL,  
FirstName nvarchar(50) NULL,  
LastName nvarchar(50) NULL,  
ContactType nvarchar(50) NULL,  
    PRIMARY KEY CLUSTERED (BusinessEntityID ASC)  
)   
AS   
-- Returns the first name, last name and contact type for the specified contact.  
BEGIN  
    DECLARE   
        @FirstName nvarchar(50),   
        @LastName nvarchar(50),   
        @ContactType nvarchar(50);  
  
    -- Get common contact information  
    SELECT   
        @BusinessEntityID = BusinessEntityID,   
@FirstName = FirstName,   
        @LastName = LastName  
    FROM Person.Person   
    WHERE BusinessEntityID = @BusinessEntityID;  
  
    SET @ContactType =   
        CASE   
            -- Check for employee  
            WHEN EXISTS(SELECT * FROM HumanResources.Employee AS e   
                WHERE e.BusinessEntityID = @BusinessEntityID)   
                THEN 'Employee'  
  
            -- Check for vendor  
            WHEN EXISTS(SELECT * FROM Person.BusinessEntityContact AS bec  
                WHERE bec.BusinessEntityID = @BusinessEntityID)   
                THEN 'Vendor'  
  
            -- Check for store  
            WHEN EXISTS(SELECT * FROM Purchasing.Vendor AS v            
                WHERE v.BusinessEntityID = @BusinessEntityID)   
                THEN 'Store Contact'  
  
            -- Check for individual consumer  
            WHEN EXISTS(SELECT * FROM Sales.Customer AS c   
                WHERE c.PersonID = @BusinessEntityID)   
                THEN 'Consumer'  
        END;  
  
    -- Return the information to the caller  
    IF @BusinessEntityID IS NOT NULL   
    BEGIN  
        INSERT @retContactInformation  
        SELECT @BusinessEntityID, @FirstName, @LastName, @ContactType;  
    END;  
  
    RETURN;  
END;  
GO  
  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(2200);  
GO  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(5);  
  
```  
  
### <a name="f-using-case-in-a-having-clause"></a>F. Usando CASE em uma cláusula HAVING  
 O exemplo a seguir usa a expressão CASE em uma cláusula HAVING para restringir as linhas retornadas pela instrução SELECT. A instrução retorna a taxa horária máxima para cada cargo na tabela `HumanResources.Employee`. A cláusula HAVING restringe os títulos aos que são mantidos por homens com uma taxa de pagamento máxima maior que 40 dólares ou por mulheres com uma taxa de pagamento máxima maior que 42 dólares.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, MAX(ph1.Rate)AS MaximumRate  
FROM HumanResources.Employee AS e  
JOIN HumanResources.EmployeePayHistory AS ph1 ON e.BusinessEntityID = ph1.BusinessEntityID  
GROUP BY JobTitle  
HAVING (MAX(CASE WHEN Gender = 'M'   
        THEN ph1.Rate   
        ELSE NULL END) > 40.00  
     OR MAX(CASE WHEN Gender  = 'F'   
        THEN ph1.Rate    
        ELSE NULL END) > 42.00)  
ORDER BY MaximumRate DESC;  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-using-a-select-statement-with-a-case-expression"></a>G. Usando uma instrução SELECT com uma expressão CASE  
 Dentro de uma instrução SELECT, a expressão CASE permite que os valores sejam substituídos no conjunto de resultados com base nos valores de comparação. O exemplo a seguir usa a expressão CASE para alterar a exibição de categorias de linhas de produtos a fim de torná-las mais compreensíveis. Quando um valor não existe, o texto "Não destinado à venda" é exibido.  
  
```  
-- Uses AdventureWorks  
  
SELECT   ProductAlternateKey, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   EnglishProductName  
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="h-using-case-in-an-update-statement"></a>H. Usando CASE em uma instrução UPDATE  
 O exemplo a seguir usa a expressão CASE em uma instrução UPDATE para determinar o valor definido para a coluna `VacationHours` para funcionários com `SalariedFlag` definido como 0. Ao subtrair 10 horas dos resultados de `VacationHours` em um valor negativo, `VacationHours` é aumentado em 40 horas; caso contrário, `VacationHours` é aumentado em 20 horas.  
  
```  
-- Uses AdventureWorks   
  
UPDATE dbo.DimEmployee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)   
       END  
    )   
WHERE SalariedFlag = 0;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [CHOOSE &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  



