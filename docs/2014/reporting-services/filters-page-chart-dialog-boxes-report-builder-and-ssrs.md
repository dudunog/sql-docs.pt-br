---
title: Página filtros, caixas de diálogo de gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.filters.f1
- "10409"
- sql12.rtp.rptdesigner.seriesgroupproperties.filters.f1
- "10401"
- sql12.rtp.rptdesigner.chartproperties.filters.f1
- "10165"
ms.assetid: fab97b2f-d53f-42f2-900c-c159653d89ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 268ca47f33e8e2514b297c2bb2a30eb77b7a8f08
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109138"
---
# <a name="filters-page-chart-dialog-boxes-report-builder-and-ssrs"></a>Página Filtros, caixas de diálogo de Gráficos (Construtor de Relatórios e SSRS)
  Clique em **filtros** no:  
  
-   caixa de diálogo**Propriedades do Grupo de Categorias** para filtrar pontos de dados em uma série agrupada por categoria.  
  
-   caixa de diálogo**Propriedades do Gráfico** para definir as opções de filtragem do gráfico.  
  
-   caixa de diálogo**Propriedades do Grupo de Séries** para limitar o número de séries no grupo selecionado.  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Clique para adicionar uma nova cláusula de filtro à lista.  
  
 **Delete (excluir)**  
 Clique para excluir a cláusula de filtro selecionada da lista.  
  
 **Seta para cima**  
 Clique para mover o filtro selecionado para cima na lista.  
  
 **Seta para baixo**  
 Clique para mover o filtro selecionado para baixo na lista.  
  
 **Expressão**  
 Digite ou escolha a expressão à qual deseja aplicar um filtro. Clique no botão expressão (**FX**) para editar a expressão.  
  
 **Tipo de dados**  
 Escolha o tipo de dados para **Valor**. Sempre que possível, escolha um tipo de dados correspondente ao tipo de dados de **Expressão**.  
  
 Os valores em **Expressão** e **Valor** devem ser avaliados como o mesmo tipo de dados. Por exemplo, se a opção **Expressão** for definida como um campo que tem o tipo de dados System.Int32 e **Valor** como 7, na lista suspensa, escolha **Inteiro**.  
  
 Se a opção de tipo de dados necessária não estiver na lista suspensa, escreva uma expressão para converter o valor no tipo de dados correto. Para obter mais informações, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
 **Operador**  
 Selecione o operador que será usado para comparar a expressão e o valor.  
  
 **Valor**  
 Digite a expressão ou valor com o qual avaliar a expressão em **Expressão**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar filtros de conjunto de dados, filtros de região e filtros de grupo &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
