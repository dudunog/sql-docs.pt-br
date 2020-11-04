---
title: Especificar um intervalo do eixo (Construtor de Relatórios) | Microsoft Docs
description: Saiba como alterar o número de rótulos e marcas de escala no eixo das categorias (x) em um gráfico definindo o intervalo do eixo no Construtor de Relatórios.
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b756d7db3a41787da2a9a1a30f1c82b9a72317c
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907174"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Especificar um intervalo do eixo (Construtor de Relatórios e SSRS)
Saiba como alterar o número de rótulos e marcas no eixo das categorias (x) em um gráfico, definindo o intervalo do eixo um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] .
 
No eixo de valor (normalmente, o eixo y), os intervalos do eixo fornecem uma medida consistente dos pontos de dados no gráfico. 

Mas no eixo de categoria (normalmente, o eixo x), às vezes, um intervalo de eixo automático resulta em categorias sem rótulos de eixo. Você pode especificar o número de intervalos que deseja na propriedade Intervalo do eixo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] calcula o número de intervalos no tempo de execução, com base nos dados do conjunto de resultados. Para obter mais informações sobre como os intervalos de eixo são calculados, consulte [Formatação de rótulos de eixo de um gráfico](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  

Para tentar definir o intervalo do eixo com dados de exemplo, confira o [Tutorial: Adicionar um gráfico de colunas ao relatório (Construtor de Relatórios)](../tutorial-add-a-column-chart-to-your-report-report-builder.md).
  
> [!NOTE]  
>  O eixo de categoria geralmente é o eixo horizontal ou o eixo x. No entanto, para os gráficos de barras, o eixo de categoria é o vertical ou eixo y.  
>
> Este tópico não se aplica a:
>-   valores de data ou hora no eixo de categoria. Por padrão, os valores de **DateTime** são exibidos como dias. Você pode especificar um intervalo de data ou hora diferente, como um mês ou o intervalo de tempo. Para obter mais informações, consulte [Formatar rótulos de eixo como datas ou moedas](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
>-  Gráficos de pizza, rosca, funil ou pirâmide, que não têm eixos. 
  
## <a name="to-show-all-the-category-labels-on-the-x-axis"></a>Para mostrar todos os rótulos de categorias no eixo x  

Neste gráfico de coluna, o intervalo de rótulos horizontal é definido como Auto.

![Captura de tela da visualização do gráfico de colunas do construtor de relatórios com o intervalo do eixo x definido como Automático.](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-auto.png)
  
1.  Clique com o botão direito do mouse no eixo da categoria e clique em **Propriedades do Eixo Horizontal**.   

    ![Captura de tela de um gráfico de colunas do construtor de relatórios mostrando como definir rótulos do eixo x.](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-labels.png)
  
2.  Na caixa de diálogo **Propriedades do Eixo Horizontal** > guia **Opções de Eixo** , defina **Intervalo** como **1** para mostrar cada rótulo do grupo de categorias. Para mostrar alternadamente o rótulo dos grupo de categorias no eixo x, digite **2**. 

     ![Captura de tela de um gráfico de colunas do construtor de relatórios mostrando como definir o intervalo do eixo x como um.](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-interval-one.png)
  
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]
     
     Agora, o gráfico de colunas exibe todos os seus rótulos do eixo horizontal.
     
     ![Captura de tela da visualização do gráfico de colunas do construtor de relatórios mostrando os rótulos do eixo x.](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-one.png)
     
     > [!NOTE]  
     >  Quando você define um intervalo do eixo, todos os rótulos automáticos são desabilitados. Se um valor para o intervalo do eixo for especificado, poderá ocorrer um comportamento imprevisível do rótulo, dependendo da quantidade de categorias existentes no eixo de categoria.  

## <a name="change-the-label-interval-in-properties-pane"></a>Alterar o intervalo de rótulo no painel Propriedades

Também é possível definir o intervalo de rótulo no painel Propriedades.

1.  No modo de exibição de design de relatório, clique no gráfico e selecione os rótulos do eixo horizontal.

3. No painel Propriedades, defina LabelInterval como **1**.

    ![Captura de tela do gráfico de colunas do construtor de relatórios mostrando como definir o intervalo dos rótulos.](../../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    O gráfico tem a mesma aparência no modo design. 
    
5.  Clique em **Executar** para visualizar o relatório.

    ![Captura de tela da visualização do gráfico de colunas do construtor de relatórios mostrando um intervalo de rótulos como um.](../../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Agora o gráfico exibe todos os seus rótulos.
  
## <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>Para habilitar um cálculo do intervalo de variáveis em um eixo  

Por padrão, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] define o intervalo do eixo como Auto. Este procedimento explica como redefini-lo para as configurações padrão. 
  
1.  Clique com o botão direito do mouse no eixo do gráfico que deseja alterar e clique em **Propriedades do Eixo**. 
  
2.  Na caixa de diálogo **Propriedades do Eixo Horizontal** > guia **Opções de Eixo** , defina **Intervalo** como **Automático**. O gráfico exibirá o número ideal de rótulos de categorias que podem se ajustar ao longo do eixo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Classificar os dados em uma região de dados (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções de Eixo &#40;Construtor de Relatórios e SSRS&#41;](/previous-versions/sql/)   
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Plotar dados em um eixo secundário &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
