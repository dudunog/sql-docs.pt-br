---
title: Explorando os modelos de cesta de compras (tutorial intermediário de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: da1c9cb7-6c32-4b9b-96ec-ecea772aeb77
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8a7b2f97cbda0594698c6cbaa68019a6493f1e74
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63224603"
---
# <a name="exploring-the-market-basket-models-intermediate-data-mining-tutorial"></a>Explorando os modelos de cesta de compras (Tutorial de mineração de dados intermediário)
  Agora que você criou o `Association` modelo, pode explorá-lo usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de associação na guia **Visualizador do modelo de mineração** do designer de mineração de dados. Este tutorial orienta você a usar o visualizador para explorar relacionamentos entre itens. O visualizador ajuda você a ver rapidamente quais produtos tendem a aparecer juntos e a obter uma ideia geral dos padrões emergentes.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de associação contém três guias: **regras**, **conjuntos**de itens e **rede de dependências**. Como cada guia revela uma exibição ligeiramente diferente dos dados, quando estiver explorando o modelo, normalmente você alternará entre os painéis diferentes várias vezes à medida que for procurando por ideias.  
  
-   [Guia rede de dependências](#bkmk_DepNet)  
  
-   [Guia conjuntos de itens](#bkmk_Itemsets)  
  
-   [Guia regras](#bkmk_Rules)  
  
-   [Visualizador de Conteúdo Genérico](#bkmk_ContentViewer)  
  
 Para este tutorial, você começará na guia **rede de dependências** e usará a guia **regras** e a guia **conjuntos** de itens para aprofundar sua compreensão das relações reveladas no visualizador. Você também usará o **Visualizador de árvore de conteúdo genérica da Microsoft** para recuperar estatísticas detalhadas para regras ou conjuntos de itens individuais.  
  
##  <a name="dependency-network-tab"></a><a name="bkmk_DepNet"></a>Guia rede de dependências  
 Com a guia **rede de dependências** , você pode investigar a interação dos diferentes itens no modelo. Cada nó do visualizador representa um item, enquanto que as linhas entre eles representam as regras. Selecionando um nó, você pode ver quais outros nós preveem o item selecionado ou quais itens o item atual prevê. Em alguns casos, há uma associação bidirecional entre itens, significando que eles geralmente aparecem na mesma transação. Você pode fazer referência à legenda de cores na parte inferior da guia para determinar a direção da associação.  
  
 Uma linha conectando dois itens significa que é provável que esses itens apareçam em uma transação juntos. Em outras palavras, é provável que os clientes comprem esses itens juntos. O controle deslizante está associado à probabilidade da regra. Mova o controle deslizante para cima ou para baixo para filtrar associações fracas, o que significa regras com probabilidade baixa.  
  
 O grafo rede de dependências mostra as regras de paridade, que podem ser representadas logicamente como uma >B, o que significa que, se o produto A for comprado, o produto B será provavelmente. O grafo não pode mostrar regras do tipo AB->C. Se você mover o controle deslizante para mostrar todas as regras e ainda assim não ver linhas no gráfico, significa que não há regras de pares que atendam aos critérios dos parâmetros do algoritmo.  
  
 Você também pode localizar nós pelo nome, digitando as primeiras letras do nome do atributo. Para obter mais informações, consulte [Caixa de diálogo Localizar Nó &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/find-node-dialog-box-mining-model-viewer.md).  
  
#### <a name="to-open-the-association-mode-in-the-microsoft-assocaition-rules-viewer"></a>Para abrir o modo Associação no Visualizador de Regras de Associação da Microsoft  
  
1.  Em **Gerenciador de soluções**, clique duas vezes na estrutura de associação.  
  
2.  No Designer de Mineração de Dados, clique na guia **Visualizador do Modelo de Mineração** .  
  
3.  Selecione associação na lista de modelos de mineração na lista suspensa **modelo de mineração** .  
  
#### <a name="to-navigate-the-dependency-graph-and-locate-specific-nodes"></a>Para navegar no grafo de dependências e localizar nós específicos  
  
1.  Na guia **Visualizador do modelo de mineração** , clique na guia **rede de dependência** .  
  
2.  Clique em **ampliar** várias vezes, até que você possa exibir facilmente os rótulos para cada nó.  
  
     Por padrão, o gráfico exibe todos os nós visíveis. Em um modelo complexo, pode haver muitos nós, fazendo com que cada nó fique muito pequeno.  
  
3.  Clique no **+** sinal no canto inferior direito do visualizador e mantenha o botão do mouse pressionado para deslocar-se pelo grafo.  
  
4.  No lado esquerdo do visualizador, arraste o controle deslizante para baixo, movendo-o de **todos os links** (o padrão) para a parte inferior do controle deslizante.  
  
5.  O visualizador atualiza o gráfico para mostrar somente a associação mais forte, entre os itens Pneu de Passeio e Tubo de Pneu de Passeio.  
  
6.  Clique no nó rotulado **tubo de aro de passeio = existente**.  
  
     O gráfico é atualizado para realçar somente os itens com uma forte relação com esse item. Observe a direção da seta entre os dois itens.  
  
7.  No lado esquerdo do visualizador, arraste o controle deslizante para cima novamente, movendo-o da parte inferior para a parte intermediária.  
  
     Observe as mudanças ocorridas na seta que conecta os dois itens.  
  
8.  Selecione **Mostrar nome do atributo somente** na lista suspensa na parte superior do painel rede de dependência.  
  
     Os rótulos de texto do gráfico são atualizados para mostrarem somente o nome do modelo.  
  
 [Voltar ao início](#bkmk_DepNet)  
  
##  <a name="itemsets-tab"></a><a name="bkmk_Itemsets"></a>Guia conjuntos de itens  
 Em seguida, você aprenderá mais sobre as regras e conjuntos de itens gerados pelo modelo para os produtos Pneu de Passeio e Tubo de Pneu de Passeio. A guia **conjuntos** de itens exibe três partes importantes de informações relacionadas aos conjuntos de elementos que o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de associação descobre:  
  
-   **Suporte:** O número de transações nas quais o conjunto ocorre.  
  
-   **Tamanho:** O número de itens no conjunto.  
  
-   **Itens:** Uma lista dos itens incluídos em cada conjunto.  
  
 Dependendo como os parâmetros do algoritmo são definidos, o algoritmo poderia gerar muitos conjuntos de itens. Cada conjunto de itens retornado no visualizador representa as transações nas quais um item foi vendido. Usando os controles na parte superior da guia **conjuntos** de itens, você pode filtrar o visualizador para mostrar apenas os conjuntos de itens que contêm um tamanho mínimo e conjunto de suporte especificados.  
  
 Se você estiver trabalhando com um modelo de mineração diferente e se nenhum conjunto de itens estiver listado, isso quer dizer que nenhum conjunto de itens atendeu aos critérios dos parâmetros do algoritmo. Nesse cenário, você poderá alterar os parâmetros do algoritmo para permitir que conjuntos de itens tenham um suporte inferior.  
  
#### <a name="to-filter-the-itemsets-that-are-shown-in-the-viewer-by-name"></a>Para filtrar os conjuntos de itens mostrados no visualizador por nome  
  
1.  Clique na guia **conjuntos** de itens do visualizador.  
  
2.  Na caixa **Filtrar conjunto** , digite `Touring Tire`e, em seguida, clique fora da caixa.  
  
     O filtro retornará todos os itens que contêm essa cadeia de caracteres.  
  
3.  Na lista **Mostrar** , selecione **Mostrar somente nome do atributo**.  
  
4.  Marque a caixa de seleção **Mostrar nome longo** .  
  
     A lista de conjuntos de itens é atualizada para mostrar somente os conjuntos de itens que contêm a cadeia de caracteres Pneu de Passeio. O nome longo do conjunto de itens inclui o nome da tabela que contém o atributo e o valor de cada item.  
  
5.  Desmarque a caixa de seleção **Mostrar nome longo** .  
  
     A lista de conjuntos de itens é atualizada para mostrar somente o nome curto.  
  
 Os valores na coluna de **suporte** indicam o número de transações para cada conjunto. Uma transação para um conjunto de itens significa uma compra que incluiu todos os itens do conjunto de itens.  
  
 Por padrão, o visualizador lista os conjuntos de itens na ordem decrescente por suporte. Você pode clicar nos cabeçalhos das colunas para classificar por uma coluna diferente, como o tamanho ou o nome do conjunto de itens. Se você estiver interessado em aprender mais sobre as transações individuais incluídas em um conjunto de itens, poderá detalhar a partir dos conjuntos de itens para os casos individuais. As colunas de estrutura dos resultados do detalhamento são o nível de renda do cliente e a ID do cliente, que não foram usados no modelo.  
  
#### <a name="to-view-details-for-an-itemset"></a>Para exibir detalhes de um conjunto de itens.  
  
1.  Na lista de conjuntos de itens, clique no título de coluna **conjunto** para classificar por nome.  
  
2.  Localize o item, `Touring Tire` (sem o segundo item).  
  
3.  Clique com o botão direito do `Touring Tire`mouse no item, selecione **detalhar**e, em seguida, selecione **colunas de modelo e estrutura**.  
  
     A caixa de diálogo **detalhar** exibe as transações individuais usadas como suporte para esse conjunto.  
  
4.  Expanda a tabela aninhada, vAssocSeqLineItems, para exibir a lista real de compras da transação.  
  
#### <a name="to-filter-itemsets-by-support-or-size"></a>Para filtrar conjuntos de itens por suporte ou tamanho  
  
1.  Limpe qualquer texto que possa estar na caixa **conjunto do filtro** . Não é possível usar um filtro de texto junto com um filtro numérico.  
  
2.  Na caixa de **suporte mínimo** , digite 100 e clique no plano de fundo do visualizador.  
  
     A lista de conjuntos de itens é atualizada para mostrar somente os conjuntos de itens com suporte de pelo menos 100.  
  
 [Voltar ao início](#bkmk_DepNet)  
  
##  <a name="rules-tab"></a><a name="bkmk_Rules"></a>Guia regras  
 A guia **regras** exibe as informações a seguir relacionadas às regras que o algoritmo encontra.  
  
-   **Probabilidade:** A *probabilidade* de uma regra, definida como a probabilidade do item à direita, dado o item do lado esquerdo.  
  
-   **Importância:** Uma medida da utilidade de uma regra. Um valor maior significa uma regra melhor.  
  
     A importância é oferecida para ajudar você a medir a utilidade de uma regra, pois a probabilidade apresentada de forma isolada pode ser falsa. Por exemplo, se todas as transações contiverem uma garrafa d'água -- talvez a garrafa d'água seja adicionada a cada carrinho automaticamente como parte de uma promoção -- o modelo criaria uma regra prevendo que a garrafa d'água teria uma probabilidade 1. Baseada somente na probabilidade, essa regra é bastante precisa, mas não oferece informações úteis.  
  
-   **Regra:** A definição da regra. Para um modelo de cesta básica, uma regra descreve uma combinação específica de itens.  
  
 Cada regra pode ser usada para prever a presença de um item em uma transação com base na presença de outros itens. Assim como na guia **conjuntos** de itens, você pode filtrar as regras para que apenas as regras mais interessantes sejam mostradas. Se você estiver trabalhando com um modelo de mineração que não tenha regras, talvez queira alterar os parâmetros do algoritmo para diminuir o limite de probabilidade para regras.  
  
#### <a name="to-see-only-rules-that-include-the-mountain-200-bicycle"></a>Para ver somente as regras que incluem a bicicleta Mountain-200  
  
1.  Na guia **Visualizador do modelo de mineração** , clique na guia **regras** .  
  
2.  Na caixa **regra de filtro** , digite `Mountain-200`.  
  
     Desmarque a caixa de seleção **Mostrar nome longo** .  
  
3.  Na lista **Mostrar** , selecione **Mostrar somente nome do atributo**.  
  
     O visualizador exibirá apenas as regras que contêm as palavras "`Mountain-200`". A probabilidade da regra indica a probabilidade de que, quando alguém comprar uma `Mountain-200` bicicleta, essa pessoa também comprará o outro produto listado.  
  
 As regras são classificadas por probabilidade em ordem decrescente, mas você pode clicar nos títulos de coluna para alterar a ordem de classificação. Se você estiver interessado em descobrir mais detalhes sobre uma determinada regra, poderá usar o detalhamento para exibir os casos de suporte.  
  
#### <a name="to-view-cases-that-support-a-particular-rule"></a>Para exibir casos que dão suporte a uma determinada regra  
  
1.  Na guia **regras** , clique com o botão direito do mouse na regra que você deseja exibir.  
  
2.  Selecione **Drill-through**e, em seguida, selecione **apenas colunas de modelo**ou **colunas modelo e estrutura**.  
  
     A caixa de diálogo **detalhar** fornece um resumo da regra na parte superior do painel e uma lista de todos os casos que foram usados como dados de suporte para a regra.  
  
 [Voltar ao início](#bkmk_DepNet)  
  
##  <a name="generic-content-tree-viewer"></a><a name="bkmk_ContentViewer"></a>Visualizador de árvore de conteúdo genérica  
 Esse visualizador pode ser usado em todos os modelos, independentemente do algoritmo ou do tipo de modelo. O **Visualizador de árvore de conteúdo genérica da Microsoft** está disponível na lista suspensa **Visualizador** .  
  
 Uma árvore de conteúdo é uma representação de um modelo de mineração como uma série de nós, em que cada nó representa conhecimento adquirido sobre alguns subconjuntos de dados. O nó pode conter um padrão, um conjunto de regras, um cluster ou a definição de um intervalo de datas que compartilham características semelhantes. O conteúdo exato do nó difere segundo o algoritmo e o tipo do atributo previsível; no entanto, a representação geral do conteúdo é a mesma. É possível expandir os nós para consultar um maior número de detalhes, assim como copiar o conteúdo de qualquer um deles para a Área de Transferência.  
  
#### <a name="to-view-details-about-the-rule-by-using-the-content-viewer"></a>Para exibir detalhes sobre a regra usando o visualizador de conteúdo  
  
1.  Na guia **Visualizador do modelo de mineração** , selecione **Visualizador de árvore de conteúdo genérica da Microsoft** na lista **Visualizador** .  
  
2.  No painel Legenda de Nó, navegue até a parte inferior da lista e clique no último nó.  
  
     O visualizador mostra conjuntos de itens primeiro e regras em seguida, mas não os agrupa. O modo mais fácil de localizar um nó específico é criar uma consulta de conteúdo. Para obter mais informações, consulte [Exemplos de consulta de um modelo associação](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
3.  No painel Detalhes do Nó, revise o valor de NODE_TYPE e NODE_DESCRIPTION.  
  
     Um tipo de nó 8 é uma regra e um tipo de nó 7 é um conjunto de itens. Para uma regra, o valor de NODE_DESCRIPTION mostra as condições que compõem a regra. Para conjunto de itens, o valor de NODE_DESCRIPTION mostra os itens incluídos no conjunto de itens.  
  
 Você também pode criar uma consulta de conteúdo para obter estatísticas detalhadas sobre as regras. Para obter mais informações sobre o conteúdo do modelo de mineração e como interpretá-lo, consulte [conteúdo do modelo de mineração para modelos de associação &#40;&#41;de mineração de dados de Analysis Services ](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Voltar ao início](#bkmk_DepNet)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Filtrando uma tabela aninhada em um modelo de mineração &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Lição 3: Criando um cenário de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)   
 [Lição 4: Criando um cenário de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)   
 [Algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Referência técnica do algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)  
  
  
