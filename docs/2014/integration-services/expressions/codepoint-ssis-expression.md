---
title: CODEPOINT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10d2eeb6991c0c75e8dbe8102f94148f60f0a361
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62769364"
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (Expressão SSIS)
  Retorna o ponto de código Unicode do caractere da extrema esquerda de uma expressão de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caracteres cujo caractere da extrema esquerda será avaliado.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_UI2  
  
## <a name="remarks"></a>Comentários  
 *character_expression* deve ter o tipo de dados DT_WSTR.  
  
 CODEPOINT retornará um resultado nulo se *character_expression* for nulo ou uma cadeia de caracteres vazia.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa um literal de cadeia de caracteres. O resultado de retorno é 77, o ponto de código Unicode para M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 Este exemplo usa uma variável. Se **Name** for Roda Dianteira de Passeio, o resultado de retorno será 84, o ponto de código de Unicode para T.  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
