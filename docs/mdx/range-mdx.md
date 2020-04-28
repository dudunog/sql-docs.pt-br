---
title: ': (Intervalo) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6afc3a73b958062bd6472153b2452bc0e3fa6cfc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020623"
---
# <a name="-range-mdx"></a>: (Intervalo) (MDX)


  Executa uma operação definida que retorna um conjunto ordenado naturalmente, com dois membros especificados como pontos de extremidade, e todos os membros entre os dois membros especificados incluídos como membros do conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="return-value"></a>Valor retornado  
 Um conjunto que contém os membros especificados e todos os membros entre os membros especificados.  
  
## <a name="remarks"></a>Comentários  
 Ambos os parâmetros devem especificar membros dentro do mesmo nível e hierarquia de uma determinada dimensão. Se ambos os parâmetros especificarem o mesmo membro, o operador **: (Range)** retornará um conjunto que contém apenas o membro especificado. Se o primeiro parâmetro for nulo, o conjunto irá conter todos os membros desde o início do nível do membro especificado no segundo parâmetro até e incluindo esse membro. Se o segundo parâmetro for nulo, o conjunto irá conter todos os membros do membro especificado no primeiro parâmetro até e incluindo o último membro no mesmo nível.  
  
 Esse operador de conjunto não tem nenhum equivalente funcional no MDX.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
