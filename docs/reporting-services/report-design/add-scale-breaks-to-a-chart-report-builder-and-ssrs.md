---
title: Adicionar quebras de escala a um gráfico (Construtor de Relatórios) | Microsoft Docs
description: Saiba como usar uma quebra de escala para exibir dois intervalos distintos na mesma área do gráfico no Construtor de Relatórios.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5bf77e72c4b8ac84d57668ebcf960ed8b926ba6e
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462330"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>Adicionar quebras de escala a um gráfico (Construtor de Relatórios e SSRS)

  Uma quebra de escala é uma faixa desenhada em uma área de plotagem de um gráfico para indicar uma quebra de continuidade entre os valores altos e baixos em um eixo de valor (normalmente, o vertical, ou eixo y). Use uma quebra de escala para exibir dois intervalos distintos na mesma área do gráfico.  
  
 ![Gráfico com quebra de escala](../../reporting-services/report-design/media/rs-multipledatarangeschart-scalebreak.gif "Gráfico com quebra de escala")  
  
> [!NOTE]  
>  Não é possível especificar onde posicionar a quebra de escala no gráfico. O gráfico usa seus próprios cálculos com base nos valores do conjunto de dados para determinar se há separação suficiente entre os intervalos de dados para desenhar uma quebra de escala no eixo de valor (eixo y) em tempo de execução.  
  
 Um exemplo de gráfico com quebras de escala está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>Para habilitar quebras de escala no gráfico  
  
1.  Clique com o botão direito do mouse no eixo vertical e clique em **Propriedades do Eixo**. A caixa de diálogo **Propriedades VerticalAxis** é aberta.  
  
2.  Marque a caixa de seleção **Habilitar quebras de escala** .  
  
### <a name="to-change-the-style-of-the-scale-break"></a>Para alterar o estilo da quebra de escala  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique com o botão direito do mouse no eixo y do gráfico. As propriedades do objeto do eixo y (denominado Eixo do Gráfico, por padrão) são exibidas no painel Propriedades.  
  
3.  Na seção **Escala** , expanda a propriedade ScaleBreakStyle.  
  
4.  Altere os valores das propriedades ScaleBreakStyle, como BreakLineType e Spacing. Para obter mais informações sobre propriedades de quebra de escala, consulte [Exibindo uma série com vários intervalos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md).  

## <a name="next-steps"></a>Próximas etapas

[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Formatando um gráfico](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[Caixa de diálogo Propriedades do Eixo, Opções de Eixo](https://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
