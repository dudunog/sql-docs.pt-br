---
title: REVERSE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ce882ae32718f634efb6b2f39ed397dfb9cbf785
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62897326"
---
# <a name="reverse-ssis-expression"></a>REVERSE (Expressão SSIS)
  Retorna uma expressão character na ordem inversa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere a ser invertida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 O argumento *character_expression* deve ter o tipo de dados DT_WSTR.  
  
 REVERSE retornará um resultado nulo se *character_expression* for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa um literal de cadeia de caracteres. O resultado de retorno é "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 Este exemplo usa uma variável. Se **Name** contiver Touring Bike, o resultado de retorno será "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
