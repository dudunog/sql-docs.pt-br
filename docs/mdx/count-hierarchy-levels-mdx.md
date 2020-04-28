---
title: Contagem (níveis de hierarquia) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17fe804de8bf2c20581ca5c00bee3a28dbce4d55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68045214"
---
# <a name="count-hierarchy-levels-mdx"></a>Count (Níveis de hierarquia) (MDX)


  Retorna o número de níveis na hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 Retorna o número de níveis em uma hierarquia, incluindo o nível `[All]`, se aplicável.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão é resolvido apenas na hierarquia visível. Por exemplo, `Measures.Levels.Count` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma contagem do número de níveis na hierarquia Categorias de Produtos definida pelo usuário no cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Contagem de &#40;de dimensões&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Contar &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Contagem &#40;definida&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
