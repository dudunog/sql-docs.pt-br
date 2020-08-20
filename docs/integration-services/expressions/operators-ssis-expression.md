---
description: Operadores (Expressão SSIS)
title: Operadores (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2c4ddb9dad3a1b6c922201906628ad3b6d25f94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477472"
---
# <a name="operators-ssis-expression"></a>Operadores (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Esta seção descreve os operadores que a linguagem de expressão fornece e a precedência e a associação de operadores usados pelo avaliador de expressão.  
  
 A tabela a seguir lista os tópicos sobre os operadores desta seção.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[Conversão &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md)|Converte uma expressão de um tipo de dados para um tipo de dados diferente.|  
|[&#40;&#41; &#40;Parênteses&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/parentheses-ssis-expression.md)|Identifica a ordem de avaliação de expressões.|  
|[+ &#40;Adicionar&#41; &#40;SSIS&#41;](../../integration-services/expressions/add-ssis.md)|Soma duas expressões numéricas.|  
|[+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)|Concatena duas expressões.|  
|[+ &#40;Subtrair&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/subtract-ssis-expression.md)|Subtrai a segunda expressão numérica da primeira.|  
|[+ &#40;Negar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/negate-ssis-expression.md)|Nega uma expressão numérica.|  
|[&#42; &#40;Multiplicar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/multiply-ssis-expression.md)|Multiplica duas expressões numéricas.|  
|[/ (Dividir) &#40;Expressão SSIS&#41;](../../integration-services/expressions/divide-ssis-expression.md)|Divide a primeira expressão numérica pela segunda.|  
|[% &#40;Módulo&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/modulo-ssis-expression.md)|Fornece o resto inteiro após dividir a primeira expressão numérica pela segunda.|  
|[&#124;&#124; &#40;OR lógica&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)|Executa uma operação OR lógica.|  
|[&& &#40;AND lógico&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)|Executa uma operação AND lógica.|  
|[\! &#40;NOT lógico&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|Nega um operando booliano.|  
|[&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|Executa uma operação OR de bit a bit de dois valores de inteiro.|  
|[^ &#40;OR exclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|Executa uma operação OR de bit a bit exclusiva de dois valores inteiros.|  
|[& &#40;AND bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)|Executa uma operação AND de bit a bit de dois valores de inteiro.|  
|[~ &#40;NOT bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|Executa uma negação bit a bit de um inteiro.|  
|[== &#40;Igual&#41; &#40;Expressão do SSIS&#41;](../../integration-services/expressions/equal-ssis-expression.md)|Executará uma comparação para determinar se duas expressões são iguais.|  
|[\!= &#40;Diferente&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/unequal-ssis-expression.md)|Executará uma comparação para determinar se duas expressões não forem iguais.|  
|[&#62; &#40;Maior que&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é maior que a segunda.|  
|[&#60; &#40;Menor que&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/less-than-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é menor que a segunda.|  
|[&#62;= &#40;Maior ou igual a&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é maior que ou igual à segunda.|  
|[&#60;= &#40;Menor ou igual a&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é menor que ou igual à segunda.|  
|[? : &#40;Condicional&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/conditional-ssis-expression.md)|Retorna uma de duas expressões baseadas na avaliação de uma expressão booliana.|  
  
 Para obter informações sobre a colocação de cada operador na hierarquia de precedência, consulte [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [Exemplos de expressões avançadas do Integration Services](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
