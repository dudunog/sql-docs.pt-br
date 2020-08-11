---
title: Especificar cores consistentes em gráficos com várias formas – Construtor de Relatórios – SSRS | Microsoft Docs
description: Saiba como a escolha de cores de um gráfico de formas resulta no mapeamento de cada cor na paleta para um ponto de dados no conjunto de dados.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d0c02b81c5ce7ea5363cf119c3a3618efd78f2aa
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83688972"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>Especificar cores consistentes em gráficos com várias formas (Construtor de Relatórios e SSRS)
  Em gráficos sem formas em um relatório paginado, o [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] seleciona uma nova cor na paleta com base no índice da série no gráfico. Por exemplo, a primeira série do gráfico é mapeada para a primeira cor da paleta. No entanto, esse comportamento é diferente em gráficos com forma. Em gráficos com forma, todas as cores da paleta são mapeadas para um ponto de dados no conjunto de dados. Por exemplo, o ponto de dados 1 é mapeado para a primeira cor da paleta, o ponto de dados 2 é mapeado para a segunda paleta de cores e assim por diante.  
  
 Caso não tenha nenhum valor, um ponto de dados é omitido na exibição de um gráfico com forma. Isso significa que o ponto de dados deixa de ser colorido. Por exemplo, se o ponto de dados 2 tiver um valor igual a zero, o ponto de dados 1 será mapeado para a primeira cor da paleta e o ponto 3, para a segunda cor da paleta. Essa abordagem é útil porque os pontos vazios no conjunto de dados de um gráfico de pizza não necessariamente usam uma cor da paleta quando o ponto vazio não precisa ser desenhado.  
  
 Como efeito colateral, quando vários gráficos de pizza são exibidos em um relatório, os gráficos de pizza podem exibir cores diferentes dos pontos de dados com o mesmo agrupamento da categoria. Para resolver isso, você precisa definir cores individuais mapeadas para um grupo de categorias, e não valores de dados individuais. A maneira como você faz isto vai depender se os gráficos de formas são minigráficos em uma tabela ou matriz, ou se eles são gráficos de formas no próprio relatório.  
  
 Como a legenda é conectada à série, todas as cores especificadas para a série serão mostradas automaticamente na legenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>Para especificar cores consistentes em minigráficos de várias formas em uma tabela ou matriz  
  
1.  Clique no gráfico para exibir o painel Dados do Gráfico.  
  
2.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em uma categoria e clique em **Propriedades de Grupos de Categorias**.  
  
3.  Na guia Geral, na caixa **Sincronizar grupos em** , clique no nome da categoria para a qual você gostaria de sincronizar cores e clique em **OK**.  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>Para especificar cores consistentes em vários gráficos com forma  
  
1.  Clique com o botão direito do mouse fora do corpo do relatório e selecione **Propriedades do Relatório**.  
  
2.  Em **Código**, digite o seguinte código na caixa de texto.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  Você precisará substituir as cadeias de caracteres "Color1" por cores próprias. É possível usar cores nomeadas, por exemplo "Vermelho" ou usar valor hexadecimal de seis dígitos que representam a cor como "#FFFFFF" para preto. Se tiver mais de três cores definidas, você precisará estender a matriz de cores para que o número de cores na matriz corresponda ao número de pontos do gráfico com forma. É possível adicionar novas cores à matriz especificando uma lista separada por vírgulas dos valores da cadeia de caracteres que contêm cores nomeadas ou representações hexadecimais das cores.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Clique com o botão direito do mouse no gráfico com forma e selecione **Propriedades da Série**.  
  
5.  Em **Preenchimento**, clique no botão **Expressão** (*fx*) para editar a expressão de acordo com a propriedade **Cor** .  
  
6.  Digite a seguinte expressão em que "MyCategoryField" é o campo exibido na área **Grupos de Categorias** :  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Adicionar estilos de bisel, alto-relevo e textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Adicionar pontos vazios a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
