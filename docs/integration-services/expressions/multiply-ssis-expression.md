---
title: '* (Multiplicar) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8d322ff646d4908f968c068def3d2ca10d4c6a15
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86904881"
---
# <a name="-multiply-ssis-expression"></a>* (Multiplicar) (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Multiplica duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression1, numeric_expression2*  
 É qualquer expressão válida de um tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentários  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo multiplica literais numéricos.  
  
```  
5 * 6.09  
```  
  
 Este exemplo multiplica valores na coluna **ListPrice** por 10%.  
  
```  
ListPrice * .10  
```  
  
 Este exemplo subtrai o resultado de uma expressão da coluna **ListPrice** . A variável **Discount%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
