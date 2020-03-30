---
title: AND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- "TRUE"
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb5211a2d45ef1a5495d1df57143190f1d5f6419
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67927377"
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Combina duas expressões boolianas e retorna **TRUE** quando ambas as expressões são **TRUE**. Quando mais de um operador lógico é usado em uma instrução, os operadores **AND** são avaliados primeiro. É possível alterar a ordem de avaliação usando parênteses.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida que retorna um valor booliano: **TRUE**, **FALSE** ou **UNKNOWN**.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Retorna TRUE quando as duas expressões são TRUE.  
  
## <a name="remarks"></a>Comentários  
 O gráfico a seguir mostra os resultados ao comparar valores TRUE e FALSE usando o operador AND.  
  
||TRUE|FALSE|DESCONHECIDO|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|DESCONHECIDO|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**UNKNOWN**|DESCONHECIDO|FALSE|DESCONHECIDO|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-and-operator"></a>a. Usando o operador AND  
 O exemplo seguinte seleciona informações sobre funcionários que têm o título de `Marketing Assistant` e mais de `41` horas de férias disponíveis.  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. Usando o operador AND em uma instrução IF  
 Os exemplos seguintes mostram como usar AND em uma instrução IF. Na primeira instrução, `1 = 1` e `2 = 2` são verdadeiros; portanto, o resultado é true. No segundo exemplo, o argumento `2 = 17` é falso; portanto, o resultado é false.  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
