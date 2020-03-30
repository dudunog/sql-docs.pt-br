---
title: Como vincular várias regiões de dados ao mesmo conjunto de dados (Construtor de Relatórios) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d282c2c84060fb205dc0421d531a5fe23003b77e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081962"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>Vinculando várias regiões de dados ao mesmo conjunto de dados (Construtor de Relatórios e SSRS)

É possível adicionar várias regiões de dados a um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fornecer exibições diferentes do mesmo conjunto de dados de relatório. Por exemplo, você pode desejar exibir dados em uma tabela e também exibi-los visualmente em um gráfico. Para isso, você deve usar expressões e escopos idênticos para as expressões de filtro, de classificação e de grupo apropriadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Para usar um gráfico e uma tabela ou matriz para exibir os mesmos dados, é útil entender as similaridades entre uma tabela e gráficos de forma e gráficos de matriz e área, de barras e de colunas. Uma tabela com um único grupo de linhas pode ser exibida facilmente como um gráfico de pizza. Conforme adiciona vários grupos de linhas, você pode escolher tipos diferentes de gráficos para exibir melhor os grupos aninhados. A adição de grupos de linhas aninhados a um gráfico de pizza aumenta o número de fatias na pizza. Você deve decidir se o número de instâncias de grupo do grupo pai e do grupo filho combinadas é muito grande para ser exibido em um único gráfico de pizza. Para vários valores de grupo que são exibidos como fatias pequenas de um gráfico de pizza, é possível definir uma propriedade para que todos os valores abaixo de um determinado limite sejam exibidos como uma fatia da pizza. Para obter mais informações, consulte [Coletar fatias pequenas em um gráfico de pizza](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
 Uma tabela com vários grupos de linhas pode ser mostrada como um gráfico de colunas com vários grupos de categorias. Para obter mais informações, consulte [Exibir os mesmos dados em uma matriz e um gráfico](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md). Para obter um exemplo de uma tabela ou gráfico que representa diferentes exibições do mesmo conjunto de dados de relatório, consulte o relatório Vendas de Linha de Produtos em Exemplos de relatórios da AdventureWorks. Como a tabela e o gráfico estão vinculados ao mesmo conjunto de dados neste relatório, quando você clica no botão de classificação interativa para Nome do Funcionário na classificação da tabela Funcionários Principais, o gráfico Funcionários Principais mostra a nova ordem de classificação automaticamente. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
 Uma matriz com vários grupos de linhas e de colunas pode ser melhor exibida usando um gráfico de área, de barras ou de colunas com os grupos de categorias e de séries. Use as mesmas expressões de grupo para grupos de colunas nos grupos de matriz e de categorias no gráfico e as mesmas expressões para grupos de linhas nos grupos de matriz e de séries no gráfico. Lembre-se que o número de instâncias de grupo afeta a legibilidade do gráfico. É possível definir grupos baseados em valores de intervalo para reduzir o número de instâncias de grupo em um relatório. Para obter mais informações, consulte [Exemplos de expressões de grupo](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
## <a name="next-steps"></a>Próximas etapas

[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Tabelas, matrizes e listas](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
[Regiões de dados aninhadas](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
