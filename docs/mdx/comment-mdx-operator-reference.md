---
title: --(Comentário) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c848277505dde5fabb10247641ee6b7f955d84e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006286"
---
# <a name="comment---mdx-operator-reference"></a>Comentário-referência de operador MDX


  Indica o texto de comentário fornecido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
 Os comentários podem ser inseridos em uma linha separada, aninhados no final de uma linha de script MDX ou aninhados em uma instrução MDX. O servidor não avalia o comentário.  
  
 Use esse operador para comentários de linha única ou aninhados. Os comentários inseridos com -- são delimitados pelo caractere de nova linha.  
  
 Não há comprimento máximo para comentários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Comentário &#40;&#41;MDX](../mdx/comment-mdx.md)   
 [Comentário de&#40;&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [Referência de operador MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
