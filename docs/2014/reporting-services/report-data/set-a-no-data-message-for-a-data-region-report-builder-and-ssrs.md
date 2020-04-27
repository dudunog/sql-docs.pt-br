---
title: Definir uma mensagem Nenhum Dado para uma região de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f2660582b03a121a81976d6bbc12afc1213877c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107093"
---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>Definir uma mensagem Nenhum Dado para uma região de dados (Construtor de Relatórios e SSRS)
  Quando quiser especificar o texto que será exibido no relatório renderizado em vez de uma região de dados sem dados, defina a propriedade NoRowsMessage para uma tabela, matriz ou região de dados de lista, NoDataMessage para uma região de dados do gráfico e NoDataText para a escala de cores de um mapa. No tempo de execução, o processador do relatório executa a consulta para cada conjunto de dados em um relatório e a consulta do conjunto de dados pode não produzir nenhum conjunto de resultados. Em uma região de dados associada a um conjunto de dados vazio, você pode especificar o texto que deseja exibir em vez de exibir uma região de dados vazia. Também é possível definir a propriedade NoRowsMessage para um sub-relatório quando nenhum conjunto de dados no sub-relatório tiver dados no tempo de execução.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>Para definir a propriedade NoRowsMessage para uma tabela, matriz ou lista  
  
1.  No modo Design, clique na região de dados de tabela, matriz ou lista ou no sub-relatório na superfície de design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, digite o texto que você deseja exibir como uma mensagem no campo de `NoRowsMessage` propriedade.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>Para definir a propriedade NoDataMessage para um gráfico  
  
1.  Na exibição Design, clique no gráfico na superfície do design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, expanda o nó para `NoDataMessage`.  
  
3.  Em **legenda**, digite o texto que você deseja exibir como uma mensagem no campo `NoDataMessage` de propriedade.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>Para definir NoRowsMessage para um sub-relatório  
  
1.  Na exibição Design, clique no sub-relatório na superfície do design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, digite o texto que você deseja exibir como uma mensagem no campo de `NoRowsMessage` propriedade.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>Para definir a propriedade NoDataText para uma escala de cores para um mapa  
  
1.  Na exibição Design, clique na escala de cores no mapa para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, em `NoDataText`, digite o texto que você deseja exibir como um rótulo para cores sem valor de dados.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)   
 [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)  
  
  
