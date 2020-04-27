---
title: Exemplos de consulta de modelo Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b713d9918dabcbaabba2085710dfaa5ed5d3a33b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083276"
---
# <a name="naive-bayes-model-query-examples"></a>Exemplos de consulta de modelo Naive Bayes
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo, que fornece detalhes de padrões descobertos em análises, ou uma consulta de previsão, que usa os padrões no modelo para fazer previsões para novos dados. Você também pode recuperar metadados sobre o modelo usando uma consulta no conjunto de linhas do esquema de mineração de dados. Esta seção explica como criar essas consultas para modelos baseados no algoritmo Naive Bayes da Microsoft.  
  
 **Consultas de conteúdo**  
  
 [Obtendo metadados de modelo usando DMX](#bkmk_Query1)  
  
 [Recuperando um resumo dos dados de treinamento](#bkmk_Query2)  
  
 [Localizando mais informações sobre atributos](#bkmk_Query3)  
  
 [Usando procedimentos armazenados do sistema](#bkmk_Query4)  
  
 **Consultas de previsão**  
  
 [Prevendo resultados com o uso de uma consulta singleton](#bkmk_Query5)  
  
 [Obtendo previsões com valores de probabilidade e suporte](#bkmk_Query6)  
  
 [Prevendo associações](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Localizando informações sobre um modelo Naive Bayes  
 O conteúdo de um modelo Naive Bayes fornece informações agregadas sobre a distribuição dos valores nos dados de treinamento. Você também pode recuperar informações sobre os metadados do modelo criando consultas no conjunto de linhas do esquema de mineração de dados.  
  
###  <a name="sample-query-1-getting-model-metadata-by-using-dmx"></a><a name="bkmk_Query1"></a>Exemplo de consulta 1: obtendo metadados de modelo usando DMX  
 Ao consultar o conjunto de linhas do esquema de mineração de dados, você pode localizar metadados para o modelo. Isso pode incluir quando o modelo foi criado, quando o modelo foi processado pela última vez , o nome da estrutura de mineração em que o modelo se baseia e o nome das colunas usadas como o atributo previsível. Você também pode retornar os parâmetros que foram usados quando o modelo foi criado.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 O modelo usado para este exemplo se baseia no modelo Naive Bayes que você cria no [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md), mas foi modificado com a adição de um segundo atributo previsível e a aplicação de um filtro aos dados de treinamento.  
  
###  <a name="sample-query-2-retrieving-a-summary-of-training-data"></a><a name="bkmk_Query2"></a> Exemplo de consulta 2: Recuperando um resumo dos dados de treinamento  
 Em um modelo Naive Bayes, o nó de estatísticas marginais armazena informações agregadas sobre a distribuição dos valores nos dados de treinamento. Esse resumo é prático e você não precisa criar consultas SQL nos dados de treinamento para localizar as mesmas informações.  
  
 O exemplo a seguir usa uma consulta de conteúdo DMX para recuperar os dados do nó (NODE_TYPE = 24). Como as estatísticas são armazenadas em uma tabela aninhada, a palavra-chave FLATTENED é usada para facilitar a exibição dos resultados.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  Você deve colocar os nomes das colunas SUPPORT e PROBABILITY entre colchetes para distingui-los das palavras-chave MDX reservadas com os mesmos nomes.  
  
 Resultados parciais:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Ausente|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0.492736216|4|  
|TM_NaiveBayes|Gênero|Ausente|0|0|1|  
|TM_NaiveBayes|Gênero|F|8656|0.495081217|4|  
|TM_NaiveBayes|Gênero|M|8828|0.504918783|4|  
  
 Por exemplo, esses resultados informam o número de casos de treinamento para cada valor discreto (VALUETYPE = 4), junto com a probabilidade calculada, ajustada para valores ausentes (VALUETYPE = 1).  
  
 Para obter uma definição dos valores fornecidos na tabela NODE_DISTRIBUTION em um modelo Naive Bayes, consulte [Conteúdo do modelo de mineração para modelos Naive Bayes &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md). Para obter mais informações sobre como o suporte e os cálculos de probabilidade são afetados por valores ausentes, consulte [Valores Ausentes &#40;Analysis Services – Data Mining&#41;](missing-values-analysis-services-data-mining.md).  
  
###  <a name="sample-query-3-finding-more-information-about-attributes"></a><a name="bkmk_Query3"></a> Exemplo de consulta 3: Localizando mais informações sobre atributos  
 Como um modelo Naive Bayes frequentemente contém informações complexas sobre as relações entre atributos diferentes, a maneira mais fácil de exibir essas relações é usar o [Visualizador Naive Bayes da Microsoft](browse-a-model-using-the-microsoft-naive-bayes-viewer.md). No entanto, você pode criar consultas DMX para retornar os dados.  
  
 O exemplo a seguir mostra como retornar informações do modelo sobre um atributo específico, `Region`.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 Esta consulta retorna dois tipos de nós: o nó que representa o atributo de entrada (NODE_TYPE = 10) e nós para cada valor do atributo (NODE_TYPE = 11). A legenda do nó é usada para identificar o nó, em vez do nome do nó, porque a legenda mostra o nome e o valor do atributo.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Região|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 Algumas das colunas armazenadas nos nós são iguais àquelas que você pode obter com base nos nós de estatísticas marginais, como a pontuação de probabilidade do nó e os valores de suporte do nó. No entanto, MSOLAP_NODE_SCORE é um valor especial fornecido apenas para os nós de atributo de entrada e indica a importância relativa desse atributo no modelo. Você pode ver grande parte das mesmas informações no painel Rede de Dependências do visualizador; no entanto, o visualizador não fornece pontuações.  
  
 A seguinte consulta retorna as pontuações de importância de todos os atributos no modelo:  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 Resultados do exemplo:  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total de Filhos|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Número de Crianças na Casa|111.8122599|  
|Bike Buyer -> Região|84.51555875|  
|Bike Buyer -> Estado Civil|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 Ao navegar no conteúdo do modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md), você terá uma noção melhor de quais estatísticas devem ser interessantes. Alguns exemplos simples foram demonstrados aqui; talvez você precise executar com mais frequência várias consultas ou armazenar os resultados e processá-los no cliente.  
  
###  <a name="sample-query-4-using-system-stored-procedures"></a><a name="bkmk_Query4"></a> Exemplo de consulta 4: Usando procedimentos armazenados de sistema  
 Além de escrever suas próprias consultas de conteúdo, você pode usar alguns procedimentos armazenados de sistema do Analysis Services para explorar os resultados. Para usar um procedimento armazenado de sistema, use a palavra-chave CALL como prefixo do nome do procedimento:  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 Resultados parciais:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  Esses procedimentos armazenados de sistema destinam-se à comunicação interna entre o servidor do Analysis Services e o cliente e só devem ser usados para conveniência durante o desenvolvimento e o teste de modelos de mineração. Quando criar consultas para um sistema de produção, você sempre deverá escrever suas próprias consultas usando DMX.  
  
 Para obter mais informações sobre os procedimentos armazenados do sistema do Analysis Services, consulte [Procedimentos armazenados de Data Mining &#40;Analysis Services – Data Mining&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining).  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Usando um modelo Naive Bayes para fazer previsões  
 O algoritmo Naive Bayes da Microsoft geralmente é menos usado para previsão do que para exploração das relações entre os atributos de entrada e previsíveis. No entanto, o modelo dá suporte ao uso de funções de previsão para previsão e associação.  
  
###  <a name="sample-query-5-predicting-outcomes-using-a-singleton-query"></a><a name="bkmk_Query5"></a> Exemplo de consulta 5: Resultados de previsão que usam uma consulta singleton  
 A consulta a seguir usa uma consulta singleton para fornecer um novo valor e prever, com base no modelo, se um cliente com essas características provavelmente comprará um modelo. A maneira mais fácil de criar uma consulta singleton em um modelo de regressão é usando a caixa de diálogo **Entrada de Consulta Singleton** . Por exemplo, você pode criar a consulta DMX a seguir selecionando o modelo `TM_NaiveBayes` , escolhendo **Consulta Singleton**e selecionando valores nas listas suspensas para `[Commute Distance]` e `Gender`.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados do exemplo:  
  
|Expression|  
|----------------|  
|0|  
  
 A função de previsão retorna o valor mais provável, nesse caso, 0, o que significa que esse tipo de cliente provavelmente não comprará uma bicicleta.  
  
###  <a name="sample-query-6-getting-predictions-with-probability-and-support-values"></a><a name="bkmk_Query6"></a>Exemplo de consulta 6: obtendo previsões com valores de probabilidade e de suporte  
 Além de prever um resultado, com frequência você deseja saber o quão sólida é a previsão. A consulta a seguir usa a mesma consulta singleton que o exemplo anterior, mas adiciona a função de previsão, [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx), para retornar uma tabela aninhada que contém estatísticas que dão suporte à previsão.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados do exemplo:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 A linha final na tabela mostra os ajustes para dar suporte e probabilidade ao valor ausente. Os valores de variação e desvio padrão sempre são 0, porque modelos Naive Bayes não podem modelar valores contínuos.  
  
###  <a name="sample-query-7-predicting-associations"></a><a name="bkmk_Query7"></a>Exemplo de consulta 7: prevendo associações  
 O algoritmo Naive Bayes da Microsoft poderá ser usado para análise de associação, se a estrutura de mineração contiver uma tabela aninhada com o atributo previsível como a chave. Por exemplo, você pode criar um modelo Naive Bayes usando a estrutura de mineração criada na [Lição 3: Criar um cenário de cesta de compras &#40;Tutorial intermediário de Data Mining&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) do tutorial de mineração de dados. O modelo usado neste exemplo foi modificado para adicionar informações sobre renda e região do cliente na tabela de casos.  
  
 O exemplo de consulta a seguir mostra uma consulta singleton que prevê produtos relacionados às compras do produto, `'Road Tire Tube'`. Você pode usar essas informações para recomendar produtos a um tipo de cliente específico.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Resultados parciais:  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>Lista de funções  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. No entanto, o algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte às funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina se um nó é um filho de outro nó no modelo.|  
|[Prever &#40;DMX&#41;](/sql/dmx/predict-dmx)|Retorna um valor previsto ou conjunto de valores de uma coluna especificada.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ponderada.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Prevê associação de membro em um conjunto de dados associativo.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna Node_ID para cada caso.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para o valor previsto.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Retorna o valor de suporte para um estado especificado.|  
  
 Para ver a sintaxe de funções específicas, consulte [Referência de função de extensões de Data Mining &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica do algoritmo do Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Algoritmo do Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)   
 [Conteúdo do modelo de mineração para modelos Naive Bayes &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
