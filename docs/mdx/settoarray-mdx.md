---
title: SetToArray (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c52c2641d21c20c91ec7548cafc969e506801b08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036994"
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)


  Converte um ou mais conjuntos para uma matriz para uso em uma função definida pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 A função **SetToArray** converte um ou mais conjuntos em uma matriz para uso em uma função definida pelo usuário. O número de dimensões na matriz resultante é igual ao número de conjuntos especificados.  
  
 A expressão numérica opcional pode fornecer os valores nas células da matriz. Se uma expressão numérica não for especificada, a junção cruzada dos conjuntos será avaliada no contexto atual.  
  
 As coordenadas da célula na matriz resultante correspondem à posição dos conjuntos na lista. Por exemplo, há três conjuntos: `SA`, `SB` e `SC`. Cada um desses conjuntos tem dois elementos. A instrução MDX, `SetToArray(SA, SB, SC)`, cria a matriz tridimensional a seguir:  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  O tipo de retorno da função **SetToArray** é o tipo VARIANT, VT_ARRAY. Portanto, a saída da função **SetToArray** deve ser usada somente como entrada para uma função definida pelo usuário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma matriz.  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
