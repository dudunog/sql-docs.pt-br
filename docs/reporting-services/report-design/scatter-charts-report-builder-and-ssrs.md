---
title: Gráficos de dispersão (Construtor de Relatórios) | Microsoft Docs
description: Saiba como usar gráficos de dispersão, com valores representados por posições de ponto em um gráfico, para comparar dados agregados entre categorias no Construtor de Relatórios.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b38cf5b7ed632726fb7a67f6018f35887730f01
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255349"
---
# <a name="scatter-charts-report-builder-and-ssrs"></a>Gráficos de dispersão (Construtor de Relatórios e SSRS)
  Um gráfico de dispersão exibe uma série como um conjunto de pontos. Os valores são representados pela posição dos pontos no gráfico. As categorias são representadas por diferentes marcadores no gráfico. Normalmente, os gráficos de dispersão são usados para comparar dados agregados por categorias. Para obter mais informações sobre como adicionar dados a um gráfico de dispersão, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
 A ilustração a seguir mostra um exemplo de gráfico de dispersão.  
  
 ![Gráfico de dispersão](../../reporting-services/report-design/media/rs-scatterchart.gif "Gráfico de dispersão")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Bolha.** Os gráficos de bolhas exibem a diferença entre dois valores de um ponto de dados baseado no tamanho da bolha. Quanto maior a bolha, maior a diferença entre os dois valores.  
  
-   **Bolha em 3D**. Um gráfico de bolhas exibido em 3D.  
  
## <a name="data-considerations-for-a-scatter-chart"></a>Considerações de dados para um gráfico de dispersão  
  
-   Normalmente, os gráficos de dispersão são usados para exibir e comparar valores numéricos, como dados científicos, estatísticos e de engenharia.  
  
-   Use o gráfico de dispersão quando quiser comparar grandes números de pontos de dados sem considerar o tempo. Quanto mais dados você inserir em um gráfico de dispersão, melhor serão as comparações que você pode criar.  
  
-   O gráfico de bolhas requer dois valores (superior e inferior) por ponto de dados.  
  
-   Os gráficos de dispersão são ideais para controlar a distribuição de valores e clusters de pontos de dados. Este será o melhor tipo de gráfico se o seu conjunto de dados contiver muitos pontos (por exemplo, milhares de pontos). Exibir várias séries em um gráfico de pontos causa uma distração visual e deve ser evitado. Neste cenário, considere o uso de um gráfico de linha.  
  
-   Por padrão, os gráficos de dispersão exibem pontos de dados como círculos. Se você tiver várias séries em um gráfico de dispersão, considere a possibilidade de alterar o marcador de cada ponto para outras formas, como quadrado, triângulo, losango, etc.  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)  
  
  
