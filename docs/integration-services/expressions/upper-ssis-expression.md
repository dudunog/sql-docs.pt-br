---
title: UPPER (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e5a444d6dea225f37b8640fd642d91ae83618d5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297341"
---
# <a name="upper-ssis-expression"></a>UPPER (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna uma expressão de caractere depois de converter caracteres minúsculos em maiúsculos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere para converter para caracteres maiúsculos.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 UPPER só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de UPPER executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 UPPER retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo converte um literal de cadeia de caracteres para caracteres maiúsculos. O resultado de retorno é "Hello".  
  
```  
UPPER("hello")  
```  
  
 Este exemplo converte o primeiro caractere na coluna **FirstName** para um caractere maiúsculo. Se **FirstName** for anna, o resultado de retorno será "A". Para obter mais informações, consulte [SUBSTRING &#40;Expressão do SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 Este exemplo converte o valor na variável **PostalCode** escrever em caracteres de letra maiúscula. Se **PostalCode** for k4b1s2, o resultado de retorno será "K4B1S2".  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [LOWER &#40;Expressão SSIS&#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
