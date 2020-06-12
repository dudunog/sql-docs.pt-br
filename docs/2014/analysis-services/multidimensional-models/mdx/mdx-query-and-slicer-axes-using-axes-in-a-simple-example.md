---
title: Usando eixos de consulta e de segmentação em um exemplo simples (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- query axis [MDX]
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 324f082fd6659592e56af65680bd4aa623c625d9
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546228"
---
# <a name="using-query-and-slicer-axes-in-a-simple-example-mdx"></a>Usando eixos de consulta e slicer em um exemplo simples (MDX)
  O exemplo simples apresentado neste tópico ilustra os fundamentos de como especificar e usar eixos de consulta e slicer.  
  
## <a name="the-cube"></a>O cubo  
 Um cubo, chamado CuboTeste, possui duas dimensões simples nomeadas Rota e Tempo. Cada dimensão tem apenas uma hierarquia de usuário, chamadas respectivamente Rota e Tempo. Como as medidas do cubo fazem parte da dimensão Medidas, esse cubo possui três dimensões no total.  
  
## <a name="the-query"></a>A consulta  
 A consulta serve para fornecer uma matriz com a qual a medida Pacotes pode ser comparada por rotas e horas.  
  
 No exemplo de consulta MDX a seguir, as hierarquias Rota e Tempo são os eixos de consulta e a dimensão Medidas é o eixo de slicer. A função [Members](/sql/mdx/members-set-mdx) indica que a linguagem MDX usará os membros da hierarquia ou do nível para construir um conjunto. O uso da função `Members` significa que você não terá que declarar explicitamente cada membro de uma hierarquia específica ou um nível em uma consulta MDX.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>O resultado  
 O resultado é uma grade que identifica o valor da medida Pacotes em cada intersecção das dimensões de eixo COLUMNS e ROWS. A tabela a seguir mostra como seria essa grade.  
  
||aérea|marítima|  
|-|---------|---------|  
|1º trimestre|60|50|  
|2º trimestre|45|45|  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando o conteúdo de um eixo de consulta &#40;&#41;MDX](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Especificando o conteúdo de um eixo da segmentação &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
