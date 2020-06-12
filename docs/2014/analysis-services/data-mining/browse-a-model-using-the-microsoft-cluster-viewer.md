---
title: Procurar um modelo usando o Visualizador de cluster da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clusters [Analysis Services]
- discrimination [Analysis Services]
- names [Analysis Services], clusters
- Microsoft Cluster Viewer
- mining model content, viewing
- comparing clusters
- viewing clusters
- displaying clusters
- data mining [Analysis Services], clusters
- Cluster Viewer [Analysis Services]
- mining models [Analysis Services], clusters
ms.assetid: 591fe30b-d88f-4a71-94d4-4a3907fc275d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 98ab519dd75d6d491d80e790e9afe06833c5597b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525428"
---
# <a name="browse-a-model-using-the-microsoft-cluster-viewer"></a>Procurar um modelo usando o Visualizador de Cluster da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador de cluster no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo de clustering. O algoritmo Cluster da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de segmentação para ser usado na exploração de dados para identificar anomalias nos dados e criar previsões. Para obter mais informações sobre esse algoritmo, consulte [Microsoft Clustering Algorithm](microsoft-clustering-algorithm.md).  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Cluster da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece as seguintes guias para serem usadas na exploração de modelos de mineração de cluster:  
  
-   [Diagrama de Cluster](#BKMK_Diagram)  
  
-   [Perfis de cluster](#BKMK_Profile)  
  
-   [Características do cluster](#BKMK_Characteristics)  
  
-   [Discriminação do Cluster](#BKMK_Discrimination)  
  
###  <a name="cluster-diagram"></a><a name="BKMK_Diagram"></a>Diagrama de cluster  
 A guia **Diagrama de Cluster** do Visualizador de Cluster da [!INCLUDE[msCoName](../../includes/msconame-md.md)] exibe todos os clusters existentes em um modelo de mineração. O sombreamento da linha que conecta um cluster a outro expressa o grau de semelhança entre os clusters. Um sombreamento claro ou a ausência dele indica que os clusters não são muito parecidos. Quanto mais escura a linha, maior a semelhança entre os links. É possível selecionar o número de linhas exibido no visualizador, ajustando-se o controle deslizante à direita dos clusters. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 Por padrão, a sombra representa a população do cluster. Usando as opções de **ShadingVariable** e **estado** , você pode selecionar o atributo e o par de estado que o sombreamento representa. Quanto mais escuro o sombreamento, maior a distribuição de atributo para um estado específico. A distribuição diminui conforme o sombreamento clareia.  
  
 Para renomear um cluster, clique com o botão direito do mouse em seu nó e selecione **Renomear Cluster**. Para o servidor, o nome novo é persistente.  
  
 Para copiar a seção visível do diagrama na Área de Transferência, clique em **Copiar Exibição de Gráfico**. Para copiar o diagrama completo, clique em **Copiar Gráfico Inteiro**. Também é possível aplicar o zoom usando **Mais Zoom** e **Menos Zoom**ou ainda ajustar o diagrama à tela usando **Dimensionar Diagrama para Ajustar à Janela**.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-profiles"></a><a name="BKMK_Profile"></a> Perfis de Cluster  
 A guia **Perfis de Cluster** oferece uma exibição geral dos clusters criados pelo algoritmo em seu modelo. Essa exibição mostra cada atributo, junto com a distribuição do atributo em cada cluster. Uma InfoDica de cada célula exibe as estatísticas de distribuição e uma InfoDica de cada cabeçalho de coluna exibe a população de cluster. Atributos discretos são mostrados como barras coloridas, e os atributos contínuos são mostrados como um gráfico de diamante que representa o desvio médio e padrão em cada cluster. A opção **Barras de histograma** controla o número de barras visíveis no histograma. Caso haja mais barras do que você optou por exibir, as barras mais altas serão retidas e as restantes, agrupadas em um recipiente cinza.  
  
 É possível alterar a nomenclatura padrão dos clusters e torná-la mais descritiva. Renomeie um cluster clicando com o botão direito do mouse no título da coluna e selecionando **Renomear cluster**. Você também pode ocultar clusters selecionando **Ocultar coluna**.  
  
 Para abrir uma janela que possibilite uma exibição maior e mais detalhada dos clusters, clique duas vezes em uma célula na coluna **Estados** ou em um histograma no visualizador.  
  
 Clique em um cabeçalho de coluna para classificar os atributos em ordem de importância para aquele cluster. Você também pode arrastar colunas para reordená-las no visualizador.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-characteristics"></a><a name="BKMK_Characteristics"></a> Características do Cluster  
 Para usar a guia **Características do Cluster** , selecione um cluster da lista **Cluster** . Depois de selecionado um cluster, é possível examinar as características particulares daquele cluster específico. Os atributos contidos no cluster são listados nas colunas **Variáveis** , e o estado do atributo listado é relacionado na coluna **Valores** . Os estados de atributo são listados em ordem de importância, descritos segundo a probabilidade com que aparecerão no cluster. A probabilidade é exibida na coluna **Probabilidade** .  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-discrimination"></a><a name="BKMK_Discrimination"></a>Discriminação de cluster  
 Você pode usar a guia **Distinção de Cluster** para comparar os atributos entre dois clusters. Use as listas **Cluster 1** e **Cluster 2** para selecionar os clusters a serem comparados. O visualizador determina as diferenças mais importantes entre os clusters e exibe os estados de atributo relativos às diferenças, por ordem de importância. Uma barra à direita do atributo mostra que cluster o estado favorece, e o tamanho da barra indica a intensidade desse favorecimento.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining-model-viewers.md)  
  
  
