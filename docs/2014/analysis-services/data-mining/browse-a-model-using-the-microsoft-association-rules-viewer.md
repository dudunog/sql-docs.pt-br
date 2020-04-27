---
title: Procurar um modelo usando o Visualizador de regras de associação da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7c3764d18d26d739023bbbb744236273e5cfd1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086154"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Procurar um modelo usando o Visualizador de Regras de Associação da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador de regras de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] associação no exibe modelos de mineração criados com [!INCLUDE[msCoName](../../includes/msconame-md.md)] o algoritmo de associação. O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de associação para ser utilizado na criação de modelos de mineração de dados que você pode usar para análise de cesta básica. Para obter mais informações sobre esse algoritmo, consulte [Microsoft Association Algorithm](microsoft-association-algorithm.md).  
  
 A seguir estão as principais razões por usar o algoritmo de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   Encontrar conjuntos de itens que descrevem itens que são localizados normalmente junto em uma transação.  
  
-   Descobrir regras que preveem a presença de outros itens em uma transação baseado em itens existentes.  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Para ver como criar, explorar e usar um modelo de mineração Associação, consulte [Lição 3: Criando um cenário de cesta de compras &#40;Tutorial intermediário de mineração de dados&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] inclui as guias a seguir:  
  
-   [Conjuntos de Itens](#BKMK_Itemsets)  
  
-   [Regras](#BKMK_Rules)  
  
-   [Rede de Dependência](#BKMK_Dependency)  
  
 Cada guia contém a caixa de seleção **Mostrar Nome Longo** , que você pode usar para mostrar ou ocultar a tabela da qual o conjunto de itens se origina na regra ou no conjunto de itens.  
  
###  <a name="itemsets"></a><a name="BKMK_Itemsets"></a>Conjuntos  
 A guia **Conjuntos de Itens** exibe a lista de conjuntos de itens que o modelo identificou como localizada normalmente junto. A guia exibe uma grade com as colunas seguintes: **Suporte**, **Tamanho**e **Conjunto de Itens**. Para obter mais informações sobre suporte, consulte [Microsoft Association Algorithm](microsoft-association-algorithm.md). A coluna **Tamanho** exibe o número de itens no conjunto de itens. A coluna **Conjunto de Itens** exibe o conjunto de itens real que o modelo descobriu. Você pode controlar o formato do conjunto de itens usando a lista **Mostrar** , que você pode definir as seguintes opções:  
  
-   **Mostrar o nome e valor de atributo**  
  
-   **Mostrar apenas o valor de atributo**  
  
-   **Mostrar apenas o nome do atributo**  
  
 Você pode filtrar o número de conjuntos de itens que são exibidos na guia utilizando **Suporte mínimo** e **Tamanho Mínimo do Conjunto de Itens**. Você pode limitar o número de conjuntos de itens exibidos cada vez mais utilizando **Filtrar Conjunto de Itens** e digitando uma característica de conjunto de itens que deve existir. Por exemplo, se você digitar "Garrafa de Água = existente", poderá limitar os conjuntos de itens à apenas aqueles que contêm uma garrafa de água. A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="rules"></a><a name="BKMK_Rules"></a>Regras  
 A guia **Regras** exibe as regras que o algoritmo de associação descobriu. A guia **Regras** inclui uma grade que contém as colunas **Probabilidade**, **Importância**e **Regra**. A probabilidade descreve como o resultado de uma regra será provavelmente. A importância é projetada para medir a utilidade de uma regra. Embora a probabilidade de ocorrência de uma regra possa ser alta, a utilidade da regra propriamente dita pode ser pouco importante. A coluna de importância trata disso. Por exemplo, se cada conjunto de itens contiver um estado específico de um atributo, uma regra que prevê o estado é trivial, embora a probabilidade seja muito alta. Quanto maior a importância, mais importante é a regra.  
  
 Você pode usar a **probabilidade mínima** e a **importância mínima** para filtrar as regras, semelhante à filtragem que você pode fazer na guia **conjuntos** de itens. Você também pode usar a **regra de filtro** para filtrar uma regra com base nos Estados dos atributos que ela contém.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="dependency-net"></a><a name="BKMK_Dependency"></a>Rede de dependências  
 A guia **Rede de Dependência** inclui um visualizador de rede de dependência. Cada nó no visualizador representa um item, como "estado = WA". A seta entre nós representa a associação entre itens. A direção da seta indica a associação entre os itens de acordo com as regras que o algoritmo descobriu. Por exemplo, se o visualizador contiver três itens, A, B e C, e C for previsto por A e B, se você selecionar o nó C, duas setas apontarão para o nó C-A para C e B para C.  
  
 O controle deslizante à esquerda do visualizador funciona como um filtro vinculado à probabilidade das regras. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo de associação da Microsoft](microsoft-association-algorithm.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining-model-viewers.md)  
  
  
