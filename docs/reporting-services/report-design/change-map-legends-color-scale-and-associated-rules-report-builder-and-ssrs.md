---
title: Alterar legendas de mapa, escala de cores e regras associadas no Construtor de Relatórios-SSRS | Microsoft Docs
description: Saiba como alterar legendas de mapa para ajudar os usuários a interpretar a visualização de dados em mapas no Construtor de Relatórios.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql13.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- sql13.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql13.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10534"
- "10516"
- sql13.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10514"
- sql13.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- "10513"
- sql13.rtp.rptdesigner.shared.mapruleslegend.f1
- sql13.rtp.rptdesigner.shared.embeddedlabels.f1
- "10510"
- "10509"
- sql13.rtp.rptdesigner.maplegendproperties.general.f1
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: deb79a6a1216f584bdbda3a54b276326e5152f01
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054234"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>Alterar legendas de mapa, escala de cores e regras associadas (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , um mapa pode conter legendas de mapa, uma escala de cores e uma escala de distância. Essas partes de um mapa ajudam os usuários a interpretar a visualização de dados no mapa.  
  
 As legendas incluem as seguintes partes de um mapa:  
  
-   **Legenda de mapa** Exibe um guia para ajudar a interpretar os dados analíticos que variam na exibição de elementos de mapas em uma camada do mapa. Um mapa pode ter várias legendas. Para cada camada do mapa, especifique qual legenda deve ser usada. Uma legenda pode fornecer um guia para mais de uma camada do mapa.  
  
-   **Escala de cores** Exibe um guia para ajudar a interpretar as cores no mapa. Um mapa tem uma escala de cores. Várias camadas podem fornecer os dados para a escala de cores.  
  
-   **Escala de distância** Exibe um guia para ajudar a interpretar a escala do mapa. Um mapa tem uma escala de distância. O valor de zoom do visor do mapa atual determina a escala de distância.  
  
 ![rs_MapElements](../../reporting-services/report-design/media/rs-mapelements.gif "rs_MapElements")  
  
##  <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a><a name="Viewport"></a> Para alterar a posição de uma legenda em relação ao visor  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>Para alterar a posição de uma legenda em relação ao visor  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse na legenda e abra a página _\<report item>_ **Propriedades**.  
  
2.  Em **Posição**, clique no local que especifica onde exibir a legenda em relação ao visor.  
  
3.  Para exibir a legenda fora do visor, selecione **Mostrar \<report item> fora do visor**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Na visualização, as legendas de mapa e a escala de cores aparecem somente quando há resultados de regras relacionadas a essa legenda. Se não houver nenhum item para exibição, a legenda não aparecerá no relatório renderizado.  
  
##  <a name="to-change-the-layout-of-a-map-legend"></a><a name="MapLegend"></a> Para alterar o layout de uma legenda de mapa  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>Para alterar o layout de uma legenda de mapa  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse na legenda e abra a página **Propriedades da Legenda** .  
  
2.  Em **Layout da legenda**, clique no layout de tabela que você deseja usar para a legenda. À medida que você clica em opções diferentes, o layout na superfície de design é alterado.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-show-or-hide-a-map-legend-title"></a><a name="MapLegendTitle"></a> Para mostrar ou ocultar um título de legenda de mapa  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>Para mostrar ou ocultar um título de legenda de mapa  
  
-   Clique com o botão direito do mouse na legenda do mapa na superfície de design e clique em **Mostrar Título da Legenda**.  
  
##  <a name="to-show-or-hide-a-color-scale-title"></a><a name="ColorScaleTitle"></a> Para mostrar ou ocultar um título de escala de cores  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>Para mostrar ou ocultar um título de escala de cores  
  
-   Clique com o botão direito do mouse na escala de cores na superfície de design e clique em **Mostrar Título da Escala de Cores**.  
  
##  <a name="to-move-items-out-of-the-first-legend"></a><a name="MoveItems"></a> Para remover itens da primeira legenda  
 Crie quantas legendas adicionais forem necessárias e atualize as regras de cada camada do mapa, especificando em qual legenda devem ser exibidos os resultados de regras.  
  
#### <a name="to-create-a-new-legend"></a>Para criar uma nova legenda  
  
-   No modo de exibição de Design, clique com o botão direito do mouse no mapa fora do visor do mapa e clique em **Adicionar Legenda**.  
  
     Uma nova legenda será exibida no mapa.  
  
#### <a name="to-display-rule-results-in-a-legend"></a>Para exibir resultados de regra em uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Clique em **Legenda**.  
  
4.  Na lista suspensa **Mostrar nesta legenda** , clique no nome da legenda na qual devem ser exibidos os resultados da regra.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-a-template-style"></a><a name="TemplateStyle"></a> Para variar cores do elemento do mapa com base em um estilo de modelo  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>Para variar cores do elemento do mapa com base em um estilo de modelo  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Clique em **Aplicar estilo do modelo**.  
  
     Um estilo de modelo especifica uma fonte, um estilo de borda e uma paleta de cores. Cada elemento do mapa recebe uma cor diferente da paleta de cores para o tema que foi especificado no Assistente de Mapa ou no Assistente de Camada do Mapa. Essa é a única opção que se aplica a camadas que não têm dados analíticos associados.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-color-palette"></a><a name="ColorPalette"></a> Para variar as cores do elemento do mapa com base em uma paleta de cores  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>Para variar as cores do elemento do mapa com base em uma paleta de cores  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Clique em **Visualizar dados usando a paleta de cores**.  
  
     Essa opção usa uma paleta interna ou personalizada que você especifica. Com base nos dados analíticos relacionados, cada elemento do mapa recebe uma cor diferente ou tom de cor da paleta.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Paleta**, na lista suspensa, selecione o nome da paleta a ser usada.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-color-ranges"></a><a name="ColorRanges"></a> Para variar as cores do elemento do mapa com base em intervalos de cores  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>Para variar as cores do elemento do mapa com base em intervalos de cores  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Clique em **Visualizar dados usando intervalos de cores**.  
  
     Essa opção, aliada às cores inicial, intermediária e final que você especifica nessa página e as opções especificadas na página **Distribuição** , divide os dados analíticos relacionados em intervalos. O processador de relatório atribui a cor apropriada a cada elemento do mapa com base nos dados associados e no intervalo em que se enquadra.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Cor inicial**, especifique a cor a ser usada para o intervalo mais baixo.  
  
6.  Em **Cor Intermediária**, especifique a cor a ser usada para o intervalo intermediário.  
  
7.  Em **Cor final**, especifique a cor a ser usada para o intervalo mais alto.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-custom-colors"></a><a name="CustomColors"></a> Para variar as cores do elemento do mapa com base em cores personalizadas  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>Para variar as cores do elemento do mapa com base em cores personalizadas  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Clique em **Visualizar dados usando cores personalizadas**.  
  
     Essa opção usa a lista de cores especificada por você. Com base nos dados analíticos relacionados, cada elemento do mapa recebe uma cor da lista. Se houver mais elementos do mapa do que cores, nenhuma cor será atribuída.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Cores personalizadas**, clique em **Adicionar** para especificar cada cor personalizada.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-set-distribution-options-for-a-legend"></a><a name="DistributionOptions"></a> Para definir as opções de distribuição de uma legenda  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>Para definir as opções de distribuição de uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Selecione a opção **Visualizar dados usando** \<rule type>. Para usar as opções de distribuição, você deve criar intervalos na página **Distribuição** com base nos dados analíticos associados à camada.  
  
4.  Clique em **Distribuição**.  
  
5.  Selecione um dos seguintes tipos de distribuição:  
  
    -   **EqualInterval**. Especifica intervalos que dividem os dados em intervalos iguais.  
  
    -   **EqualDistribution**. Especifica intervalos que dividem esses dados de forma que cada intervalo tenha um número de itens igual.  
  
    -   **Ideal**. Especifica os intervalos que ajustam automaticamente a distribuição para criar subintervalos equilibrados.  
  
    -   **Personalizado**. Especifique seu próprio número de intervalos para controlar a distribuição de valores.  
  
     Para obter mais informações sobre as opções de distribuição, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
6.  Em **Número de subintervalos**, digite o número de subintervalos a ser usado. Quando o tipo de distribuição for **Ideal**, o número de subintervalos será calculado automaticamente.  
  
7.  Em **Início do intervalo**, digite um valor de intervalo mínimo. Todos os valores menores do que esse número são iguais ao intervalo mínimo.  
  
8.  Em **Fim do intervalo**, digite um valor de intervalo máximo. Todos os valores maiores do que esse número são iguais ao intervalo máximo.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-contents-of-a-rule-legend"></a><a name="RuleLegend"></a> Para alterar o conteúdo de uma legenda de regras  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>Para alterar o conteúdo da legenda de cor, tamanho, largura ou tipo de marcador  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados que você deseja e clique em _\<map element type>_ **Regra**.  
  
3.  Verifique se a opção **Visualizar dados usando** \<*rule type*> está selecionada.  
  
4.  Em **Campo de dados**, verifique se os dados analíticos visualizados na camada estão selecionados.  
  
    > [!NOTE]  
    >  Se nenhum campo aparecer na lista suspensa, clique com o botão direito do mouse na camada e clique em **Dados da Camada** para abrir a caixa de diálogo Propriedades de Dados da Camada do Mapa, página Dados Analíticos e verificar se você especificou dados analíticos para essa camada.  
  
5.  Clique em **Legenda**.  
  
6.  Em **Mostrar nesta legenda**, selecione a legenda do mapa a ser usada para exibir os resultados da regra.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-contents-of-the-color-scale"></a><a name="ColorScale"></a> Para alterar o conteúdo da escala de cores  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>Para alterar o conteúdo da escala de cores ou de uma legenda de cor  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados desejados e clique em _\<map element type>_ **Regra de Cores**.  
  
3.  Selecione a opção de regra de cor a ser usada. Para exibir itens em uma legenda do mapa ou escala de cores, você precisa selecionar uma das opções **Visualizar dados usando** \<rule type>.  
  
4.  Em **Campo de dados**, verifique se os dados analíticos visualizados na camada estão selecionados.  
  
    > [!NOTE]  
    >  Se nenhum campo aparecer na lista suspensa, clique com o botão direito do mouse na camada e clique em **Dados da Camada** para abrir a caixa de diálogo Propriedades de Dados da Camada do Mapa, página Dados Analíticos e verificar se você especificou dados analíticos para essa camada.  
  
5.  Clique em **Legenda**.  
  
6.  Em **Opções de escala de cores**, selecione **Mostrar na escala de cores** para exibir os resultados da regra na escala de cores. Você pode especificar esta opção para mais de uma regra de cor.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-remove-all-items-from-a-legend"></a><a name="HideItems"></a> Para remover todos os itens de uma legenda  
  
#### <a name="to-hide-items-based-on-a-rule"></a>Para ocultar itens com base em uma regra  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados que você deseja e clique em _\<map element type>_ **Regra**.  
  
3.  Clique em **Legenda**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-format-of-content-in-a-legend"></a><a name="ChangeFormatItems"></a> Para alterar o formato de conteúdo em uma legenda  
 Defina as opções de legenda para a regra associada à legenda de mapa.  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>Para alterar o formato de conteúdo em uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com o botão direito do mouse na camada que tem os dados que você deseja e clique em _\<map element type>_ **Regra**.  
  
3.  Clique em **Legenda**.  
  
4.  O**Texto de legenda** exibe as palavras-chave que especificam quais dados são exibidos na legenda. Use as palavras-chave do mapa e os formatos personalizados para ajudar a controlar o formato do texto da legenda. Por exemplo, #FROMVALUE {C2} especifica um formato de moeda com duas casas decimais. Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Adicionar, alterar ou excluir um mapa ou uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Solucionar problemas de relatórios: Mapear relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
