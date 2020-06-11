---
title: Procurar um modelo usando o Visualizador de árvore da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
author: minewiskan
ms.author: owend
ms.openlocfilehash: d02a4111301dd880999bbcf9e6bea75062ef9599
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525238"
---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Procurar um modelo usando a Exibição de Árvore da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador de árvore no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe árvores de decisão que são criadas com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo árvores de decisão. O algoritmo Árvores de Decisão [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de árvore de decisão híbrido que oferece suporte tanto à classificação quanto regressão. Portanto, você também pode usar esse visualizador para exibir modelos com base no algoritmo Regressão Linear [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é usado para modelagem preditiva de atributos discretos e contínuos. Para obter mais informações sobre esse algoritmo, consulte [Referência técnica do algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md).  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_TabsPanes"></a>Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Árvores [!INCLUDE[msCoName](../../includes/msconame-md.md)] inclui as seguintes guias e painéis:  
  
-   [Árvore de decisões](#BKMK_DecisionTree)  
  
-   [Rede de Dependências](#BKMK_DependencyNetwork)  
  
-   [Legenda de Mineração](#BKMK_MiningLegend)  
  
###  <a name="decision-tree"></a><a name="BKMK_DecisionTree"></a>Árvore de decisão  
 Quando você criar um modelo de árvore de decisão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criará uma árvore separada para cada atributo previsível. Você pode ver uma árvore individual selecionando-a na lista **Árvore** da guia **Árvore de Decisão** do visualizador.  
  
 Uma árvore de decisão é composta por várias divisões, com a divisão mais importante, conforme determinado pelo algoritmo, à esquerda do visualizador no nó **Todas** . Divisões adicionais ocorrem à direita. A divisão do nó **Todas** é o mais importante porque contém a divisão mais importante, gerando condições no conjunto de dados, gerando, portanto, a primeira divisão.  
  
 É possível expandir ou recolher os nós individuais na árvore para mostrar ou ocultar as divisões que ocorrem após cada nó. Também é possível usar as opções na guia **Árvore de Decisão** para interferir na maneira de exibição da árvore. Use o controle deslizante **Mostrar Nível** para ajustar o número de níveis exibidos na árvore. Use a opção **Expansão Padrão** para definir o número padrão de níveis exibidos em todas as árvores no modelo.  
  
#### <a name="predicting-discrete-attributes"></a>Prevendo atributos discretos  
 Quando uma árvore é criada com um atributo previsível discreto, o visualizador exibe o seguinte em cada nó da árvore:  
  
-   A condição que causou a divisão.  
  
-   Um histograma que representa a distribuição dos estados do atributo previsível, ordenado por popularidade.  
  
 Você pode usar a opção **Histograma** para alterar o número de estados que são exibidos nos histogramas da árvore. Isso será útil se o atributo previsível tiver muitos estados. Os estados são exibidos em um histograma em ordem de popularidade, da esquerda para a direita; se o número de estados que você escolhe para serem exibidos for menor do que o número total de estados do atributo, os estados menos populares serão exibidos coletivamente em cinza. Para ver a contagem exata de cada estado para um nó, coloque o ponteiro do mouse sobre o nó para exibir uma Infodica ou selecione o nó para exibir seus detalhes na **Legenda de Mineração**.  
  
 A cor da tela de fundo de cada nó representa a concentração de casos do estado do atributo em particular selecionado usando a opção **Tela de Fundo** . Você pode usar essa opção para destacar nós que contêm um determinado destino no qual você está interessado.  
  
#### <a name="predicting-continuous-attributes"></a>Prevendo atributos contínuos  
 Quando uma árvore é criada com um atributo previsível contínuo, o visualizador exibe um gráfico de losangos, em vez de um histograma, para cada nó da árvore. O gráfico de losangos tem uma linha que representa o intervalo do atributo. O losango fica na posição mediana do nó, e sua largura representa a variação do atributo naquele nó. Um losango mais estreito indica que o nó pode criar uma previsão mais precisa. O visualizador também exibe a equação de regressão, usada para determinar a divisão no nó.  
  
#### <a name="additional-decision-tree-display-options"></a>Opções adicionais de exibição da Árvore de Decisão  
 Quando o detalhamento está habilitado para um modelo de árvore de decisões, você pode acessar os casos de treinamento que oferecem suporte a um nó, clicando com o botão direito do mouse no nó da árvore e selecionando **Detalhamento**. Você pode habilitar o detalhamento no Assistente de Mineração de Dados ou ajustando a propriedade de detalhamento no modelo de mineração da guia **Modelos de Mineração** .  
  
 Você pode usar as opções de zoom da guia **Árvore de Decisão** para aplicar mais ou menos zoom em uma árvore ou usar **Ajustar Tamanho** para ajustar o modelo inteiro na tela do visualizador. Se uma árvore for muito grande para ser ajustada à tela, você poderá usar a opção **Navegação**para navegar na árvore. Clicar em **Navegação** faz com que seja aberta uma janela de navegação separada na qual você pode selecionar seções do modelo a serem exibidas.  
  
 Você também pode copiar a imagem da exibição em árvore para a Área de Transferência para que possa colá-la em documentos ou em um software de manipulação de imagens. Use **Copiar Exibição de Gráfico** para copiar apenas a seção da árvore visível no visualizador ou use **Copiar Gráfico Inteiro** para copiar todos os nós expandidos na árvore.  
  
 [Voltar ao início](#BKMK_TabsPanes)  
  
###  <a name="dependency-network"></a><a name="BKMK_DependencyNetwork"></a>Rede de dependências  
 A **Rede de Dependências** exibe as dependências entre os atributos de entrada e os atributos previsíveis no modelo. O controle deslizante à esquerda do visualizador funciona como um filtro vinculado aos pontos fortes das dependências. Se você abaixar o controle deslizante, apenas os links mais importantes serão mostrados no visualizador.  
  
 Quando você selecionar um nó, o visualizador destacará as dependências específicas ao nó. Por exemplo, se você escolher um nó previsível, o visualizador também realçará cada nó que ajuda a prever o nó previsível.  
  
 Se o visualizador contiver muitos nós, você poderá procurar nós específicos usando o botão **Localizar Nó** . Clicar em **Localizar Nó** faz com que a caixa de diálogo **Localizar Nó** seja aberta, na qual você pode usar um filtro para pesquisar e selecionar nós específicos.  
  
 A legenda na parte inferior do visualizador vincula os nós de cores ao tipo de dependência no gráfico. Por exemplo, quando você seleciona um nó previsível, ele fica sombreado na cor turquesa e os nós que preveem o nó selecionado são sombreados em laranja.  
  
 [Voltar ao início](#BKMK_TabsPanes)  
  
###  <a name="mining-legend"></a><a name="BKMK_MiningLegend"></a>Legenda de mineração  
 A **Legenda de Mineração** exibe as informações a seguir quando você seleciona um nó no modelo de árvore de decisão:  
  
-   O número de casos no nó, divididos em estados do atributo previsível.  
  
-   A probabilidade de cada caso do atributo previsível do nó.  
  
-   Um histograma que inclui uma conta para cada estado do atributo previsível.  
  
-   As condições que são exigidas para alcançar um nó específico, também conhecidas como *caminho de nó*.  
  
-   Para os modelos de regressão linear, a fórmula de regressão.  
  
 Você pode encaixar e trabalhar com a **Legenda de Mineração** da mesma maneira que trabalha com o Gerenciador de Soluções.  
  
 [Voltar ao início](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo árvores de decisão da Microsoft](microsoft-decision-trees-algorithm.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](../mining-model-viewers-data-mining-model-designer.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining-model-viewers.md)  
  
  
