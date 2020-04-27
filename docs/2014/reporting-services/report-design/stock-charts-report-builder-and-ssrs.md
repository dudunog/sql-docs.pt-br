---
title: Gráficos de ações (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f75ca11e-b7f5-4ac0-ba17-fe6f82742dad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8f5b0e6ecc8dab66eb375a568fa1188549ac8ae3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104804"
---
# <a name="stock-charts-report-builder-and-ssrs"></a>Gráficos de ações (Construtor de Relatórios e SSRS)
  Um gráfico de estoque é especificamente projetado para dados financeiros ou científicos que usam até quatro valores por ponto de dados. Esses valores se alinham com os valores alto, baixo, aberto e fechado usados para plotar dados de estoque financeiro. Esse tipo de gráfico exibe valores de abertura e fechamento usando marcadores, que geralmente são linhas ou triângulos. No exemplo a seguir, os valores de abertura são mostrados pelos marcados à esquerda e os valores de fechamento são mostrados pelos marcadores à direita.  
  
 ![Gráfico de ações](../media/rs-stockchart.gif "Gráfico de ações")  
  
 Um exemplo de um gráfico de ações está disponível como um relatório de exemplo do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Report Builder. Para obter mais informações sobre como baixar este relatório de exemplo e [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]outros, consulte [Construtor de relatórios e Report Designer relatórios de exemplo](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Velas**. O gráfico de velas é uma forma especializada do gráfico de estoque, na qual as caixas são usadas para mostrar a faixa entre os valores de abertura e fechamento. Da mesma forma que o gráfico de estoque, o gráfico de velas pode exibir até quatro valores por ponto de dados.  
  
## <a name="data-considerations-for-stock-charts"></a>Considerações de dados para gráficos de estoque  
  
-   Ao apresentar muitos pontos de dados de estoque, como tendências de preço de estoque anual, é difícil distinguir entre os valores aberto, fechado, alto e baixo de cada ponto de dados. Nesse cenário, considere usar um gráfico de linhas em vez de um gráfico de estoque.  
  
-   Quando os rótulos de eixos são gerados, a rotulação geralmente começa em zero.  Em geral, os preços de estoque não flutuam no mesmo grau que os outros conjuntos de dados. Por esse motivo, talvez você queira desativar os rótulos de eixos de iniciar em zero para obter uma melhor exibição de seus dados. Para fazer isso, defina **IncludeZero** como **false** na caixa de diálogo **Propriedades do Eixo** ou na janela Propriedades. Para obter mais informações sobre como o gráfico gera rótulos de eixo, consulte [Formatação de rótulos de eixo de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece muitas fórmulas calculadas para uso com gráficos de estoque, inclusive Indicador de Preços, Índice de Força Relativa, MACD e outros.  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos de intervalo &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções do Eixo &#40;Construtor de Relatórios e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
