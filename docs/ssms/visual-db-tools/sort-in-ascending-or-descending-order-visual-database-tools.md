---
title: Classificar em ordem crescente ou decrescente
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 947ff75c1eb3f0a20b0bc3c415645254a7c4b6c4
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85976760"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>Classificar em ordem crescente ou decrescente (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode classificar os resultados da consulta em ordem crescente ou decrescente em uma ou mais das colunas do conjunto de resultados usando as palavras-chaves **ASC** ou **DESC** com a cláusula **ORDER BY** .  
  
> [!NOTE]  
> A ordem de classificação é determinada em parte pela sequência de ordenação da coluna. Você pode alterar a sequência de ordenação na [Caixa de Diálogo de Ordenação](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md).  
  
O procedimento seguinte supõe que você tenha uma consulta aberta no Designer de Consulta e Visualização que usa a cláusula ORDER BY para ordenar uma ou mais colunas.  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>Para especificar ou alterar a ordem na qual os resultados são ordenados  
  
1.  No painel [Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), clique no campo **Tipo de Classificação** para a coluna que você deseja reclassificar.  
  
2.  Escolha **Crescente** ou **Decrescente** para especificar a ordem de classificação da coluna.  
  
Note que conforme você trabalha no painel de critérios, a cláusula UNION de sua consulta é alterada para corresponder a suas ações mais recentes.  
  
> [!NOTE]  
> Ao classificar resultados em mais de uma coluna, especifique a ordem de pesquisa das colunas em relação umas às outras usando a coluna Ordem de Classificação. Para obter mais informações, consulte [Classificar várias colunas em consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
