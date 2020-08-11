---
title: Gráficos polares (Construtor de Relatórios) | Microsoft Docs
description: Descubra o uso de um gráfico polar com pontos agrupados por categoria em um círculo e valores representados pelo comprimento de um ponto do centro do círculo.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c9402d8f-202a-4cdf-949e-50f5b1d2b885
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2f0ab5d9368f96cfd54a54a3859891dc4efbe821
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689462"
---
# <a name="polar-charts-report-builder-and-ssrs"></a>Gráficos polares (Construtor de Relatórios e SSRS)
  Um gráfico polar exibe uma série como um conjunto de pontos agrupados por categoria em um círculo de 360 graus. Os valores são representados pelo comprimento do ponto, conforme medido do centro do círculo. Quanto mais distante o ponto está do centro, maior é o seu valor. São exibidos rótulos de categoria no perímetro do gráfico. Para obter mais informações sobre como adicionar dados a um gráfico polar, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Gráfico de radar**. Um gráfico de radar exibe uma série como uma linha ou área circular. Ao contrário do gráfico polar, o gráfico de radar não exibe dados em termos de coordenadas polares.  
  
## <a name="data-considerations-for-polar-charts"></a>Considerações de dados para gráficos polares  
  
-   O gráfico de radar é útil para comparações entre várias séries de dados de categoria.  
  
-   Os gráficos polares são usados com mais frequência para fazer gráficos de dados polares, nos quais cada ponto de dados é determinado por um ângulo ou uma distância.  
  
-   Os gráficos polares não podem ser combinados com qualquer outro tipo de gráfico na mesma área de gráfico.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como um gráfico de radar pode ser usado. A tabela a seguir fornece dados de amostra do gráfico.  
  
|Nome|Sales|  
|----------|-----------|  
|Arbustos|61|  
|Sementes|78|  
|Bulbos|60|  
|Árvores|38|  
|Flores|81|  
  
 Nesse exemplo, o campo Nome é colocado na área Grupos de Categorias. O campo Vendas é colocado na área Valores. O campo Vendas é agregado automaticamente para o gráfico quando você o lança. O gráfico de radar calcula onde colocar os rótulos com base no número de valores no campo Vendas, que contém cinco valores e coloca rótulos em cinco pontos equidistantes em um círculo. Se o campo Vendas continha três valores, os rótulos seriam colocados em três pontos equidistantes em um círculo.  
  
 A ilustração a seguir mostra um exemplo de um gráfico de radar baseado nos dados apresentados.  
  
 ![Gráfico de radar](../../reporting-services/report-design/media/rs-radarchart.gif "Gráfico de radar")  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
