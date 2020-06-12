---
title: Procurar um modelo usando o Visualizador de cluster de sequência da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Sequence Cluster Viewer
- clusters [Analysis Services]
- data mining [Analysis Services], sequences
- discrimination [Analysis Services]
- mining model content, viewing
- mining models [Analysis Services], sequences
- Microsoft Sequence Cluster Viewer
- sequence [Analysis Services]
- transitions [Analysis Services]
ms.assetid: 3ada00aa-da9e-488a-9f53-c3e188f81f84
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5e7262beef3e9d64a488e255fe5fd9f1b79a8837
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525183"
---
# <a name="browse-a-model-using-the-microsoft-sequence-cluster-viewer"></a>Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador de cluster de sequência no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo clustering de sequência. O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSC é um algoritmo de análise de sequência para uso na exploração de dados que contêm eventos que podem ser vinculados de acordo com caminhos ou *sequências*. Para obter mais informações sobre esse algoritmo, consulte [Algoritmo MSC](microsoft-sequence-clustering-algorithm.md).  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
> [!NOTE]  
>  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Cluster Viewer oferece funcionalidade e opções similares aos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Cluster Viewer. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Cluster da Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Cluster de Sequência da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece as seguintes guias para uso na exploração de modelos de mineração de sequência de agrupamento:  
  
-   [Diagrama de Cluster](#BKMK_Diagram)  
  
-   [Perfis de cluster](#BKMK_Profile)  
  
-   [Características do cluster](#BKMK_Characteristics)  
  
-   [Discriminação do Cluster](#BKMK_Discrimination)  
  
-   [Transições do cluster](#BKMK_Transitions)  
  
###  <a name="cluster-diagram"></a><a name="BKMK_Diagram"></a>Diagrama de cluster  
 A guia **Diagrama do Cluster** do Visualizador de Cluster de Sequência da [!INCLUDE[msCoName](../../includes/msconame-md.md)] exibe todos os clusters de um modelo de mineração. O sombreamento da linha que conecta um cluster a outro expressa o grau de semelhança entre os clusters. Um sombreamento claro ou a ausência dele indica que os clusters não são muito parecidos. Quanto mais escura a linha, maior a semelhança entre os links. É possível selecionar o número de linhas exibido no visualizador, ajustando-se o controle deslizante à direita dos clusters. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 Por padrão, a sombra representa a população do cluster. Usando as opções de **ShadingVariable** e **estado** , você pode selecionar o atributo e o par de estado que o sombreamento representa. Quanto mais escuro o sombreamento, maior a distribuição de atributo para um estado específico. A distribuição diminui conforme o sombreamento clareia.  
  
 Para renomear um cluster, clique com o botão direito do mouse em seu nó e selecione **Renomear Cluster**. Para o servidor, o nome novo é persistente.  
  
 Para copiar a seção visível do diagrama na Área de Transferência, clique em **Copiar Exibição de Gráfico**. Para copiar o diagrama completo, clique em **Copiar Gráfico Inteiro**. Também é possível aplicar o zoom usando **Mais Zoom** e **Menos Zoom**ou ainda ajustar o diagrama à tela usando **Dimensionar Diagrama para Ajustar à Janela**.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-profiles"></a><a name="BKMK_Profile"></a> Perfis de Cluster  
 A guia **Perfil de Cluster** oferece uma exibição geral dos clusters criados pelo algoritmo em seu modelo. Cada coluna após a coluna **População** na grade representa um cluster descoberto pelo modelo. A \<attribute> linha. Samples representa diferentes sequências de dados existentes no cluster, e a \<attribute> linha descreve todos os itens que o cluster contém e sua distribuição geral.  
  
 A opção **Barras de histograma** controla o número de barras visíveis no histograma. Caso haja mais barras do que você optou por exibir, as barras mais altas serão retidas e as restantes, agrupadas em um recipiente cinza.  
  
 É possível alterar a nomenclatura padrão dos clusters e torná-la mais descritiva. Renomeie um cluster clicando com o botão direito do mouse no título da coluna e selecionando **Renomear cluster**. Você pode ocultar clusters selecionando **Ocultar coluna**e também arrastar as colunas para reordená-las no visualizador.  
  
 Para abrir uma janela que possibilite uma exibição maior e mais detalhada dos clusters, clique duas vezes em uma célula na coluna **Estados** ou em um histograma no visualizador.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-characteristics"></a><a name="BKMK_Characteristics"></a> Características do Cluster  
 Para usar a guia **Características do Cluster** , selecione um cluster da lista **Cluster** . Depois de selecionado um cluster, é possível examinar as características particulares daquele cluster específico. Os atributos contidos no cluster são listados nas colunas **Variáveis** , e o estado do atributo listado é relacionado na coluna **Valores** . Os estados de atributo são listados em ordem de importância, descritos segundo a probabilidade com que aparecerão no cluster. A probabilidade é exibida na coluna **Probabilidade** .  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-discrimination"></a><a name="BKMK_Discrimination"></a>Discriminação de cluster  
 Você pode usar a guia **Discriminação do Cluster** para comparar atributos entre dois clusters, e determinar como os itens de uma sequência favorecem um cluster em detrimento de outro. Use as listas **Cluster 1** e **Cluster 2** para selecionar os clusters a serem comparados. O visualizador determina as diferenças mais importantes entre os clusters e exibe os estados de atributo relativos às diferenças, por ordem de importância. Uma barra à direita do atributo mostra que cluster o estado favorece, e o tamanho da barra indica a intensidade desse favorecimento.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="cluster-transitions"></a><a name="BKMK_Transitions"></a>Transições de cluster  
 Ao selecionar um cluster na guia **Transições do Cluster** , você pode procurar as transições entre estados de sequência no cluster selecionado. Cada nó exibido representa um estado da coluna de sequência. Uma seta representa uma transição entre dois estados e a probabilidade associada a ela. Se uma transição voltar ao nó de origem, uma seta poderá apontar de volta ao nó de origem.  
  
 Uma seta originada em um ponto representa a probabilidade de o nó ser o início de uma sequência. Uma extremidade final que conduz ao nulo representa a probabilidade de o nó vir a ser o término da sequência.  
  
 Você pode filtrar a extremidade dos nós usando o controle deslizante à esquerda da guia.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Algoritmo de clustering de sequência da Microsoft](microsoft-sequence-clustering-algorithm.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores de modelo de mineração de dados](data-mining-model-viewers.md)   
 [Procurar um modelo usando o Visualizador de Cluster da Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
  
