---
title: + (Concatenar) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9fdb6ca97e324411ca32e30eda330240fe68a564
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921283"
---
# <a name="-concatenate-ssis-expression"></a>+ (Concatenar) (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Concatena duas expressões em uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 É qualquer expressão de tipo de dados válida DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT ou DT_IMAGE.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 A expressão pode usar um ou ambos os tipos de dados DT_STR e DT_WSTR.  
  
 A concatenação dos tipos de dados DT_STR e DT_WSTR retorna um resultado do tipo DT_WSTR. O comprimento da cadeia de caracteres é a soma dos comprimentos das cadeias originais expressas em caracteres.  
  
 Somente os dados com os tipo de dados DT_STR e DT_WSTR da cadeia de caracteres ou os tipos de dados DT_TEXT, DT_NTEXT e DT_IMAGE do BLOB (Bloco de objetos binários grande) podem ser concatenados. Outros tipos de dados devem ser convertidos explicitamente a um desses tipos de dados antes de ocorrer a concatenação. Para obter mais informações sobre conversões legais entre tipos de dados, consulte [Conversão &#40;Expressão do SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Ambas as expressões devem ser do mesmo tipo de dados ou uma expressão deve ser convertida implicitamente para o tipo de dados da outra expressão. Por exemplo, se a cadeia "Order date is " e a coluna **OrderDate** forem concatenadas, os valores em **OrderDate** serão implicitamente convertidos em um tipo de dados de cadeia de caracteres. Para concatenar dois valores numéricos, ambos os valores numéricos devem ser lançados explicitamente a um tipo de dados de cadeia de caracteres.  
  
 Uma concatenação pode usar só um tipo de dados BLOB: DT_TEXT, DT_NTEXT ou DT_IMAGE.  
  
 Se qualquer elemento for nulo, o resultado será nulo.  
  
 Literais da cadeia de caracteres devem estar entre aspas.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo concatena os valores nas colunas **FirstName** e **LastName** e insere um espaço entre eles.  
  
```  
FirstName + ' ' + LastName  
```  
  
 Este exemplo concatena as variáveis **ZIPCode** e **ZIPCode+4**. Ambas as variáveis têm um tipo de dados de cadeia de caracteres. **ZIPCode+4** deve ser incluído em parênteses porque o nome da variável inclui o caractere +.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
