---
title: NextMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b852564510c6b5918c781e0c75e84e3b30aecd44
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088361"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  Retorna o próximo membro no nível que contém um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **NextMember** retorna o próximo membro, no mesmo nível, que contém o membro especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o membro Agosto de 2001 como o próximo membro para o membro Julho de 2001.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
