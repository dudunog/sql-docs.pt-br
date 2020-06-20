---
title: Classificar em ordem crescente ou decrescente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8b5cb3170ed8447627d8eb14675b8527442045aa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85000968"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>Classificar em ordem crescente ou decrescente (Visual Database Tools)
  Você pode classificar os resultados da consulta em ordem crescente ou decrescente em uma ou mais das colunas do conjunto de resultados usando as palavras-chaves `ASC` ou `DESC` com a cláusula `ORDER BY` .  
  
> [!NOTE]  
>  A ordem de classificação é determinada em parte pela sequência de ordenação da coluna. Você pode alterar a sequência de ordenação na [Caixa de Diálogo de Ordenação](visual-database-tools.md).  
  
 O procedimento seguinte supõe que você tenha uma consulta aberta no Designer de Consulta e Visualização que usa a cláusula ORDER BY para ordenar uma ou mais colunas.  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>Para especificar ou alterar a ordem na qual os resultados são ordenados  
  
1.  No painel [Critérios](criteria-pane-visual-database-tools.md), clique no campo **Tipo de Classificação** para a coluna que você deseja reclassificar.  
  
2.  Escolha **Crescente** ou **Decrescente** para especificar a ordem de classificação da coluna.  
  
 Note que conforme você trabalha no painel de critérios, a cláusula UNION de sua consulta é alterada para corresponder a suas ações mais recentes.  
  
> [!NOTE]  
>  Ao classificar resultados em mais de uma coluna, especifique a ordem de pesquisa das colunas em relação umas às outras usando a coluna Ordem de Classificação. Para obter mais informações, consulte [Classificar várias colunas em consultas &#40;Visual Database Tools&#41;](sort-multiple-columns-in-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Classificar e agrupar resultados de consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Resumir os resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
