---
title: '- (Negar) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1137fa6847cf851a6cb56ffd8a0da10032decc7a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62897405"
---
# <a name="--negate-ssis-expression"></a>- (Negação) (Expressão SSIS)
  Nega uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É qualquer expressão válida de um tipo de dados numérico. Há suporte somente para tipos de dados numéricos assinados. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *numeric_expression*.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo nega o valor da variável **Counter** e adiciona o literal numérico 50.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
