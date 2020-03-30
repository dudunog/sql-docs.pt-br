---
title: Alterar a altura da linha ou a largura da coluna (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5396ca15db85405053f8c003fb643e26b13f46fe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77078920"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Alterar a altura da linha ou a largura da coluna (Construtor de Relatórios e SSRS)
  Quando você define a altura de uma linha, você está especificando a altura máxima da linha no relatório renderizado. No entanto, por padrão, as caixas de texto na linha são definidas para crescer na vertical para acomodar seus dados em tempo de execução e isso pode fazer com que uma linha seja expandida além da altura especificada. Para definir uma altura de linha fixa, você deve alterar as propriedades da caixa de texto para que elas não se expandam automaticamente.  
  
 Quando você define a largura de coluna, você está especificando a largura máxima da coluna no relatório renderizado. As colunas não se ajustam automaticamente na horizontal para acomodar o texto.  
  
 Se uma célula em uma linha ou coluna contém um retângulo ou uma região de dados, a altura e largura mínimas da célula são determinadas pela altura e largura do item contido. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>Para alterar a altura da linha movendo os indicadores de linha  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da linha que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da linha e movê-la para cima ou para baixo para ajustar a altura da linha.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>Para alterar a altura da linha definindo as propriedades de célula  
  
1.  Na exibição Design, clique em uma célula na linha da tabela.  
  
     ![Célula selecionada em uma tabela](../../reporting-services/report-design/media/table-selectcell.png "Célula selecionada em uma tabela")  
  
2.  No painel **Propriedades** exibido, modifique a propriedade **Altura** , e clique em qualquer lugar fora do painel **Propriedades** .  
  
     ![Painel de propriedades para a célula de tabela selecionada](../../reporting-services/report-design/media/cell-propertiespane.png "Painel de propriedades para a célula de tabela selecionada")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>Para impedir que uma linha se expanda automaticamente na vertical  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Clique na alça da linha para selecioná-la.  
  
3.  No painel Propriedades, defina CanGrow como **False**.  
  
    > [!NOTE]  
    >  Se você não puder ver o painel Propriedades, no menu **Exibir** , clique em **Propriedades**.  
  
### <a name="to-change-column-width"></a>Para alterar a largura da coluna  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de coluna cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da coluna que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da coluna e movê-la para a esquerda ou direita para ajustar a largura da coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Região de dados Tablix (Construtor de Relatórios e SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 [Células, linhas e colunas da região de dados Tablix (Construtor de Relatórios) e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [Tabelas (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes (Construtor de Relatórios e SSRS)](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas (Construtor de Relatórios e SSRS)](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
