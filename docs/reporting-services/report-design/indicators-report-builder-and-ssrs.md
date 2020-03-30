---
title: Indicadores (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10545"
- "10547"
- sql13.rtp.rptdesigner.indicatorproperties.action.f1
- "10546"
- sql13.rtp.rptdesigner.indicatorproperties.validateandstates.f1
- sql13.rtp.rptdesigner.indicatorproperties.general.f1
ms.assetid: 2edbd279-be39-4d97-b1b6-ddbc5b17c422
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c2e62ec26c0019e82b3f0e37dbdd9c1539332212
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082073"
---
# <a name="indicators-report-builder-and-ssrs"></a>Indicadores (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , os indicadores são medidores pequenos que transmitem o estado de um único valor de dados em um relance. Os ícones que representam indicadores e os respectivos estados são simples e visualmente efetivos mesmo quando usados em tamanhos pequenos.  
  
 Você pode declarar indicadores em seus relatórios mostrar o seguinte:  
  
-   **Tendências** usando setas de subidas, planas (sem alteração) ou descidas.  
  
-   **Estado** usando símbolos comumente reconhecidos, como marcas de seleção e pontos de exclamação.  
  
-   **Condições** usando formas comumente reconhecidas, como semáforos e sinais.  
  
-   **Classificações** usando formas e símbolos reconhecidos comuns que mostram o progresso, como o número de quadrantes em um quadrado e estrelas.  
  
 É possível usar indicadores por si mesmos em painéis ou em relatórios de forma livre, mas são usados mais comumente em tabelas ou matrizes para visualizar dados em linhas ou colunas. O diagrama a seguir mostra uma tabela com um indicador de semáforo que transmite vendas acumuladas no ano por vendedor e território.  
   
 ![rs_IndicatorTableTrafficLight](../../reporting-services/report-design/media/rs-indicatortabletrafficlight.gif "rs_IndicatorTableTrafficLight")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece conjuntos de indicadores internos e ícones de indicador a serem usados no estado em que se encontram, mas você também pode personalizar ícones de indicador e conjuntos de indicadores individuais para atender às suas necessidades.  
  
 Para obter mais informações sobre como usar indicadores como KPIs, consulte [Tutorial: Adicionar um KPI ao seu relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md).  
  
> [!NOTE]  
>  É possível publicar indicadores separadamente de um relatório como partes do relatório. Leia mais sobre as [Partes do relatório](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="comparing-indicators-to-gauges"></a><a name="ComparingIndicatorsToGauges"></a> Comparando indicadores a medidores  
 Embora pareçam diferentes, os indicadores são medidores simples. Os indicadores e os medidores exibem um único valor de dados. As principais diferenças entre eles são elementos como quadros e ponteiros. Os indicadores têm apenas estados, ícones e (opcionalmente) rótulos. Os estados de indicadores são semelhgantes aos intervalos de medidores.  
  
 Assim como os medidores, os indicadores são posicionados dentro de um painel de medidores. Quando você deseja configurar um indicador usando a caixa de diálogo **Propriedades de Indicadores** ou o painel Propriedades, é necessário selecionar o indicador, em vez do painel. Caso contrário, as opções disponíveis se aplicarão às opções do painel de medidores e você não poderá configurar o indicador. A imagem a seguir mostra um indicador selecionado em seu painel de medidores.  
  
 ![rs_GaugePanelWithIndicator](../../reporting-services/report-design/media/rs-gaugepanelwithindicator.gif "rs_GaugePanelWithIndicator")  
  
 Dependendo do modo como você deseja descrever o valor dos dados, os medidores talvez sejam mais eficientes do que os indicadores. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
##  <a name="choosing-the-indicator-type-to-use"></a><a name="ChoosingIndicatorTypes"></a> Escolhendo o tipo de indicador a ser usado  
 O uso do conjunto de indicadores certo é essencial para a comunicação instantânea do significado dos dados, quer eles estejam em uma linha de detalhes ou em um grupo de linhas ou colunas em uma tabela ou matriz, ou sozinhos no corpo do relatório ou painel. Os conjuntos de indicadores internos têm três ou mais ícones. Os ícones variam em forma, cor ou ambos. Cada ícone comunica um estado de dados diferente.  
  
 A tabela a seguir lista os conjuntos de indicadores internos e descreve alguns de seus usos comuns.  
  
|Conjunto de indicadores|Tipo de indicador|  
|-------------------|--------------------|  
|![Rs_DirectionalIcons](../../reporting-services/report-design/media/rs-directionalicons.gif "Rs_DirectionalIcons")|Direcional: indica tendências usando setas para cima, para baixo, planas (sem alterações), de subida e descida.|  
|![Rs_SymbolIcons](../../reporting-services/report-design/media/rs-symbolicons.gif "Rs_SymbolIcons")|Símbolos: indica estados usando símbolos comumente reconhecidos, como marcas de seleção e pontos de exclamação.|  
|![Rs_ShapeIcons](../../reporting-services/report-design/media/rs-shapeicons.gif "Rs_ShapeIcons")|Forma: indica condições usando formas comuns, como sinais de tráfego e formas de losango.|  
|![rs_RatingIcons](../../reporting-services/report-design/media/rs-ratingicons.gif "rs_RatingIcons")|Classificações: indica classificações usando formas e símbolos reconhecidos comuns que mostram valores progressivos, como o número de quadrantes em um quadrado.|  
  
 Depois que você escolher um conjunto de indicadores, poderá personalizar a aparência de cada ícone indicador no conjunto definindo suas propriedades nas caixas de diálogo para indicadores ou no painel Propriedades. Você pode usar as cores internas, os ícones e os tamanhos ou as expressões para configurar indicadores.  
  
##  <a name="customizing-indicators"></a><a name="CustomizingIndicators"></a> Personalizando indicadores  
 É possível personalizar indicadores de acordo com as suas necessidades. Voc~e pode modificar os conjuntos de indicadores e o ícone indicador individual dentro de um conjunto das seguintes maneiras:  
  
-   Altere as cores de ícones de indicador. Por exemplo, talvez você queira que o esquema de cores de um conjunto de indicadores seja monocromático ou use cores diferentes do padrão.  
  
-   Altere o ícone no conjunto de indicadores. Por exemplo, talvez você queira usar os ícones de estrela, círculo e quadrado em um conjunto de indicadores.  
  
-   Especifique os valores inicial e final de um indicador. Por exemplo, talvez você queira distorcer a exibição de dados usando um ícone para 75% dos valores do indicador.  
  
-   Adicione ícones ao conjunto de indicadores. Por exemplo, talvez você queira adicionar mais ícones aos conjuntos de indicadores para diferenciar os valores de indicador de um modo mais detalhado.  
  
-   Exclua ícones do conjunto de indicadores para tornar a exibição de dados mais simples usando apenas alguns ícones.  
  
 Para obter mais informações, consulte [Alterar os ícones de indicadores e os conjuntos de indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md).  
  
##  <a name="using-indicators-in-tables-and-matrices"></a><a name="UsingIndicatorsInTablesMatrices"></a> Usando indicadores em tabelas e matrizes  
 As formas simples de indicadores os tornam ideais para uso em tabelas e matrizes. Até mesmo os indicadores pequenos são efetivos. Isso os torna úteis em detalhes ou linhas de grupo de relatórios.  
  
 O diagrama a seguir mostra um relatório com uma tabela que usa o conjunto de indicadores direcionais, **Quatro Setas (Coloridas)** , para indicar as vendas. Os ícones de indicador no relatório estão configurados para usar tons de azul, em vez das cores padrão: vermelho, amarelo e verde.  
  
 ![rs_IndicatorReportBlueArrows](../../reporting-services/report-design/media/rs-indicatorreportbluearrows.gif "rs_IndicatorReportBlueArrows")  
  
 Para obter mais informações sobre como adicionar, alterar e excluir indicadores, veja [Adicionar ou excluir um indicador &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-an-indicator-report-builder-and-ssrs.md).  
  
 Quando você adiciona um indicador a um relatório, ele é configurado para usar valores padrão. Em seguida, você pode alterar os valores para que o indicador descreva dados da maneira que desejar. Você pode alterar a aparência dos ícones de indicador, o modo como o indicador escolhe qual ícone usar e alterar os ícones usados por um conjunto de indicadores. Para obter mais informações, consulte [Alterar os ícones de indicadores e os conjuntos de indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md).  
  
 Por padrão, indicadores são configurados para usar percentuais como a unidade de medida e detectar automaticamente os valores mínimo e máximo nos dados. Cada ícone no conjunto de indicadores tem um intervalo de percentuais. O número de intervalos de percentuais depende do número de ícones no ícone definido, mas os intervalos são do mesmo tamanho e sequenciais. Por exemplo, se o conjunto de ícones tiver cinco ícones, haverá cinco intervalos de percentuais, cada um com 20 por cento em tamanho. O primeiro inicia com 0 e termina com 20, o segundo inicia com 20 e termina com 40, e assim por diante. O indicador do relatório usa o ícone do conjunto de indicadores que tem um intervalo de percentuais dentro do qual está o valor de dados do indicador. Você pode alterar o intervalo de percentuais para cada ícone do conjunto. Os valores mínimo e máximo podem ser definidos explicitamente fornecendo um valor ou uma expressão. Se preferir, altere a unidade de medida para que seja um valor numérico. Nesse caso, você não especifica mínimo ou máximo para obter os dados. Em vez disso, você fornece apenas os valores de início e término para cada ícone usado pelo indicador. Para obter mais informações, consulte [Definir e configurar unidades de medida &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-and-configure-measurement-units-report-builder-and-ssrs.md).  
  
 Os indicadores transmitem valores de dados sincronizando valores de dados de indicador dentro de um escopo especificado. Por padrão, o escopo é o contêiner pai do indicador, como a tabela ou matriz que contém o indicador. Você pode alterar a sincronização do indicador escolhendo um escopo diferente, de acordo com o layout do seu relatório. O indicador pode omitir a sincronização. Para obter mais informações, consulte [Definir o escopo da sincronização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-synchronization-scope-report-builder-and-ssrs.md).  
  
 Para obter informações gerais sobre como entender e definir escopo em relatórios, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Os indicadores usam um único valor. Se você precisar mostrar vários valores de dados, use um minigráfico ou uma barra de dados em vez de um indicador. Eles podem representar vários valores de dados, mas são simples, fáceis de entender em tamanhos pequenos e funcionam bem em tabelas e matrizes. Para obter mais informações, consulte [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
##  <a name="sizing-indicators-to-maximize-visual-impact"></a><a name="SizingIndicatators"></a> Dimensionando indicadores para maximizar o impacto visual  
 Além de cor, direção e forma, você pode usar o tamanho para maximizar o impacto visual de indicadores. Imagine um relatório que use indicadores para mostrar a satisfação do cliente com os diferentes tipos de bicicletas. O ícone usado pelo indicador pode ser configurado para tamanhos diferentes, dependendo da satisfação do cliente. Quanto maior a satisfação, maior o ícone que aparecerá no relatório. A imagem a seguir mostra um relatório de vendas de bicicletas, e os tamanhos dos ícones refletem o valor das vendas.  
  
 Use expressões para definir dinamicamente o tamanho das estrelas com base nos valores de campo usados pelo indicador. Para obter mais informações, consulte [Especificar o tamanho de um indicador usando uma expressão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md).  
  
 Para saber mais sobre gravar e usar expressões, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
##  <a name="including-indicators-and-gauges-in-gauge-panels"></a><a name="IncludingIndicatorsInGauges"></a> Incluindo indicadores e medidores em painéis de medidores  
 Os indicadores sempre são posicionados dentro de um painel de medidores. O painel de medidores é um contêiner de nível superior que pode incluir um ou mais medidores e indicadores de estado. O painel de medidores pode conter medidores filhos ou adjacentes ou indicadores. Se você usar um indicador como filho de outro indicador, poderá visualizar com mais detalhes os dados mostrando o estado do valor de dados exibido no indicador. Por exemplo, um indicador em um medidor pode exibir um círculo verde para informar que o valor no medidor aponta para os 33% superiores do intervalo de valores. Usando um medidor e um indicador lado a lado, você pode representar os dados de modos diferentes. Em todo caso, o indicador e o medidor podem usar os mesmos campos de dados ou campos de dados diferentes.  
  
 O diagrama a seguir mostra um indicador lado a lado e dentro de um indicador.  
  
 ![rs_GaugePanelWithIndicatorAndGauge](../../reporting-services/report-design/media/rs-gaugepanelwithindicatorandgauge.gif "rs_GaugePanelWithIndicatorAndGauge")  
  
 Para obter mais informações, consulte [Incluir indicadores e medidores em um painel de medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre o uso de medidores, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
##  <a name="sequence-of-indicator-states"></a><a name="SequenceIndicatorStates"></a> Sequência de estados do indicador  
 A sequência dos estados do indicador na guia **Valor e Estados** da caixa de diálogo **Propriedades do Indicador** afeta qual ícone de indicador é exibido para um valor de dados quando os valores de início e término dos estados de indicador se sobrepõem.  
  
 Isto poderá acontecer se você usar o percentual ou a unidade de medida em estado numérico. Isso é mais provável ocorrer quando você usa a unidade de medida numérica porque você forneceu valores específicos para esta medida. Isso também é mais provável de ocorrer quando você arredonda valores de dados de relatório, porque isto tende a fazer valores menos discretos.  
  
 Os cenários a seguir descrevem como a visualização de dados é afetada quando você altera a sequência dos três estados nos indicadores direcionais **3 Setas (Coloridas)** . Por padrão, a sequência é:  
  
1.  Seta vermelha para baixo  
  
2.  Seta horizontal amarela  
  
3.  Seta verde para cima  
  
 Os cenários a seguir são mostrados para quatro sequências de estado diferentes e os intervalos de valor, e como as sequências afetam a visualização de dados.  
  
 Nestes cenários, o indicador **3 Setas (Coloridas)** usa medidas de estado numéricas.  
  
|Sequência de estado|Valor de início|Valor final|  
|--------------------|-----------------|---------------|  
|Vermelho|0|3500|  
|Amarelo|3500|5\.000|  
|Verde|5\.000|10000|  
  
 A seta vermelha para baixo descreve o valor 3500 e a seta horizontal amarela, 5000.  
  
|Sequência de estado|Valor de início|Valor final|  
|--------------------|-----------------|---------------|  
|Verde|5\.000|10000|  
|Amarelo|3500|5\.000|  
|Vermelho|0|3500|  
  
 A seta horizontal amarela descreve o valor 3500 e a seta verde para cima, 5000.  
  
|Sequência de estado|Valor de início|Valor final|  
|--------------------|-----------------|---------------|  
|Verde|5\.000|10000|  
|Vermelho|0|3500|  
|Amarelo|3500|5\.000|  
  
 A seta vermelha para baixo descreve o valor 3500 e a seta verde para cima, 5000.  
  
|Sequência de estado|Valor de início|Valor final|  
|--------------------|-----------------|---------------|  
|Amarelo|3500|5\.000|  
|Vermelho|0|3500|  
|Verde|5\.000|10000|  
  
 A seta amarela para baixo agora descreve os valores 3500 e 5000.  
  
 Em resumo, a avaliação inicia e a parte superior da lista de estado de indicador e o relatório exibem o ícone de indicador associado com o primeiro estado de indicador que tem um intervalo de valor nos quais os dados se ajustam. Ao alterar a sequência dos estados do indicador, você poderá, portanto, afetar a visualização de valores de dados.  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> Tópicos de instruções  
 Esta seção lista os procedimentos que mostram como adicionar, alterar e excluir indicadores; como configurar e personalizar indicadores e como usar indicadores em medidores.  
  
-   [Adicionar ou excluir um indicador &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-an-indicator-report-builder-and-ssrs.md)  
  
-   [Alterar os ícones de indicadores e os conjuntos de indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)  
  
-   [Definir e configurar unidades de medida &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-and-configure-measurement-units-report-builder-and-ssrs.md)  
  
-   [Definir o escopo da sincronização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-synchronization-scope-report-builder-and-ssrs.md)  
  
-   [Especificar o tamanho de um indicador usando uma expressão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md)  
  
-   [Incluir indicadores e medidores em um painel de medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
