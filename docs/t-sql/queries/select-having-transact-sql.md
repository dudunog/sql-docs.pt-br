---
title: HAVING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a574e3f7348c4641665b067193c54604145386c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76315606"
---
# <a name="select---having-transact-sql"></a>SELECT – HAVING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica um critério de pesquisa para um grupo ou uma agregação. HAVING pode ser usado somente com a instrução SELECT. HAVING é normalmente usado com uma cláusula GROUP BY. Quando GROUP BY não for usado, haverá um único grupo agregado e implícito.   
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>Argumentos  
\<search_condition> especifica um ou mais predicados aos quais os grupos e/ou as agregações devem corresponder. Para obter mais informações sobre critérios de pesquisa e predicados, consulte [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Os tipos de dados **text**, **image** e **ntext** não podem ser usados em uma cláusula HAVING.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir que usa uma cláusula simples `HAVING` recupera o total para cada `SalesOrderID` da tabela `SalesOrderDetail` que excede `$100000.00`.  
  
```sql
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir usa uma cláusula `HAVING` para recuperar a `SalesAmount` total que excede `80000` para cada `OrderDateKey` da tabela `FactInternetSales`.  
  
```sql
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

