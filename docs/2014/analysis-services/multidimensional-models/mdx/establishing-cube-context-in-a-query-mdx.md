---
title: Estabelecendo o contexto de cubo em uma consulta (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
author: minewiskan
ms.author: owend
ms.openlocfilehash: 72ae6e19f879651feb47841d70b444e9f845c74e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546508"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>Estabelecendo o contexto de cubo em uma consulta (MDX)
  Toda consulta MDX é executada em um contexto de cubo especificado. Esse contexto define os membros que são avaliados pelas expressões da consulta.  
  
 Na instrução SELECT, a cláusula FROM determina o contexto de cubo. Esse contexto pode ser o cubo inteiro ou apenas um subcubo dele. Ao especificar o contexto de cubo usando a cláusula FROM, você pode usar funções adicionais para expandir ou restringir esse contexto.  
  
> [!NOTE]  
>  As instruções SCOPE e CALCULATE também permitem administrar o contexto de cubo a partir de um script MDX. Para obter mais informações, consulte [Conceitos básicos do script MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md).  
  
## <a name="from-clause-syntax"></a>Sintaxe da cláusula FROM  
 A sintaxe a seguir descreve a cláusula FROM:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 Nessa sintaxe, observe que é a cláusula `<SELECT subcube clause>` que descreve o cubo ou o subcubo no qual a instrução SELECT é executada.  
  
 Um exemplo simples de uma cláusula FROM seria aquele executado no cubo inteiro de exemplo Adventure Works. Essa cláusula FROM teria o seguinte formato:  
  
```  
FROM [Adventure Works]  
```  
  
 Para obter mais informações sobre a cláusula FROM na instrução MDX SELECT, consulte [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select).  
  
## <a name="refining-the-context"></a>Refinando o contexto  
 Embora a cláusula FROM especifique o contexto de cubo como um único cubo, ela não impede que você trabalhe com os dados de mais de um cubo ao mesmo tempo.  
  
 Você pode usar a função MDX [LookupCube](/sql/mdx/lookupcube-mdx) para recuperar dados de cubos fora do contexto de cubo. Além disso, funções, como a função [Filter](/sql/mdx/filter-mdx) , estão disponíveis para permitir a restrição temporária do contexto durante a avaliação da consulta.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
