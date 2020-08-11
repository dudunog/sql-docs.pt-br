---
title: Adicionar pontos vazios a um gráfico (Construtor de Relatórios) | Microsoft Docs
description: Especifique pontos vazios em um gráfico. Esses pontos são calculados no Construtor de Relatórios tirando a média dos pontos de dados anteriores e seguintes que contêm um valor.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: afdcb8a6d464484fb6f294cb4d7943659e32e7f1
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255659"
---
# <a name="add-empty-points-to-a-chart-report-builder-and-ssrs"></a>Adicionar pontos vazios a um gráfico (Construtor de Relatórios e SSRS)
Valores nulos são mostrados no gráfico como espaços vazios ou lacunas entre os pontos de dados em uma série. Nos relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , pontos vazios são pontos de dados que podem ser inseridos em um espaço vazio criado por valores nulos.  
  
 Por padrão, pontos vazios são calculados pela média dos pontos de dados anteriores e seguintes que contêm um valor. Você pode alterar isso para que todos os pontos vazios sejam inseridos como zero.  
  
 Para obter mais informações, consulte [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-empty-points-on-a-chart"></a>Para especificar pontos vazios em um gráfico  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique com o botão direito do mouse na série que contém valores nulos. As propriedades da série são exibidas no painel Propriedades.  
  
3.  Expanda o nó **EmptyPoint** .  
  
4.  Selecione um valor de cor para a propriedade Color.  
  
5.  No nó **EmptyPoint** , expanda o nó Marker.  
  
6.  Selecione um tipo de marcador para a propriedade MarkerType.  
  
    > [!NOTE]  
    >  Você deve selecionar um tipo de marcador para adicionar pontos vazios a um gráfico de barras, colunas ou de dispersão. No entanto, para gráficos de área, linha e radar, a seleção de um tipo de marcador é opcional porque o gráfico preenche o espaço vazio ou a lacuna sem precisar da especificação de um marcador.  
  
7.  Defina o valor do ponto vazio.  
  
    1.  No painel Propriedades, expanda o nó **CustomAttributes** .  
  
    2.  Defina a propriedade EmptyPointValue. Para inserir pontos vazios em uma média dos pontos de dados anteriores e seguintes, selecione **Média**. Para inserir pontos vazios em zero, selecione **Zero**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Adicionar quebras de escala a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
