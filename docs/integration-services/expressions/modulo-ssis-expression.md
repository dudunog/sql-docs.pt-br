---
description: (Módulo) (Expressão SSIS)
title: (Módulo) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14ea6b261c63b06d5e6b3fbeb77822c0d3c6836f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457197"
---
# <a name="modulo-ssis-expression"></a>(Módulo) (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Fornece o resto inteiro após dividir a primeira expressão numérica pela segunda.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 É a expressão numérica a ser dividida. *dividend* pode ser qualquer expressão numérica válida. Para obter mais informações, consulte [Tipos de Dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md)  
  
 *divisor*  
 É a expressão numérica pela qual dividir o dividendo. *divisor* pode ser qualquer expressão numérica com exceção de zero.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentários  
 Ambas as expressões devem ser avaliadas como tipos de dados inteiro assinados ou não assinados.  
  
 Se qualquer operando for nulo, o resultado será nulo.  
  
 Módulo zero não é válido.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo calcula o módulo de dois literals numéricos. O resultado é 3.  
  
```  
42 % 13  
```  
  
 Esse exemplo calcula o módulo da coluna **SalesQuota** e um literal numérico.  
  
```  
SalesQuota % 12  
```  
  
 Esse exemplo calcula o módulo de duas variáveis numéricas **Sales$** e **Month**. A variável **Sales$** deve estar entre colchetes porque o nome inclui o caractere $. Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
@[Sales$] % @Month  
```  
  
 Esse exemplo usa o operador de módulo para determinar se o valor da variável **Value** é par ou ímpar e se usa o operador condicional para retornar uma cadeia que descreve o resultado. Para obter mais informações, consulte [? : &#40;Condicional&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/conditional-ssis-expression.md).  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
