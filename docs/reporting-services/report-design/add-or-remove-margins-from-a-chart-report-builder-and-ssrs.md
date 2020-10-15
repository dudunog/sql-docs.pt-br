---
title: Adicionar ou remover margens de um gráfico (Construtor de Relatórios) | Microsoft Docs
description: Adicione ou remova margens de um gráfico de colunas ou dispersão no Construtor de Relatórios. Aprimore a legibilidade ou a aparência de relatórios paginados.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bbe5af103737cb9b4a5ba7e063f19b9cd6c1da41
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935364"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>Adicionar ou remover margens de um gráfico (Construtor de Relatórios e SSRS)
Para os tipos de gráfico de Colunas e de Dispersão nos relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o gráfico automaticamente adiciona margens laterais nas extremidades do eixo x. Nos tipos de gráfico de Barras, o gráfico adiciona automaticamente margens laterais nas extremidades do eixo y. Em todos os outros tipos de gráfico, as margens laterais não são adicionadas. Não é possível alterar o tamanho da margem.  
  
 Este tópico não se aplica aos tipos de gráfico de pizza, anel, funil ou pirâmide.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-enable-or-disable-side-margins"></a>Para habilitar ou desabilitar as margens laterais  
  
1.  Clique com o botão direito do mouse no eixo e selecione **Propriedades do Eixo**. A caixa de diálogo **Propriedades do Eixo Vertical** ou **Horizontal** é exibida.  
  
2.  Na página **Opções do Eixo** , defina a propriedade **Margens laterais** :  
  
    -   **Automático** O gráfico determinará se deve ser adicionada uma margem lateral com base no tipo de gráfico.  
  
    -   **Desabilitado** Os gráficos de barra, coluna e dispersão não terão nenhuma margem lateral.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções de Eixo &#40;Construtor de Relatórios e SSRS&#41;](/previous-versions/sql/)   
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
