---
title: Propriedades de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5ed1c47faafeb0c680e6afb6f8e509c426760da2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940714"
---
# <a name="data-mining-properties"></a>Propriedades de mineração de dados
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de mineração de dados listadas nas tabelas a seguir. Para obter mais informações sobre as propriedades de servidor adicionais e como defini-las, consulte [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** Somente modo de servidor multidimensional  
  
## <a name="non-specific-category"></a>Categoria não específica  
 `AllowSessionMiningModels`  
 Uma propriedade Booleana que indica se podem ser criados modelos de mineração de sessão.  
  
 O valor padrão para essa propriedade é false, o que indica que modelos de mineração de sessão não podem ser criados.  
  
 `AllowAdHocOpenRowsetQueries`  
 Uma propriedade Booleana que indica se consultas ad hoc abertas de conjunto de linhas são permitidas.  
  
 O valor padrão para essa propriedade é false, o que indica que as consultas abertas de conjuntos de linhas não são permitidas durante uma sessão.  
  
 `AllowedProvidersInOpenRowset`  
 Uma propriedade de cadeia de caracteres que identifica quais fornecedores são permitidos em um conjunto de linhas aberto, consistindo de uma lista de ProgIDs ou [All] de fornecedores separada por vírgula/ponto-e-vírgula.  
  
 `MaxConcurrentPredictionQueries`  
 Uma propriedade de inteiro de 32 bits assinada que define o número máximo de consultas de previsão simultâneas.  
  
## <a name="algorithms-category"></a>Categoria de algoritmos  
 `Microsoft_Association_Rules\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Association_Rules está habilitado.  
  
 `Microsoft_Clustering\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Clustering está habilitado.  
  
 `Microsoft_Decision_Trees\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ DecisionTrees está habilitado.  
  
 `Microsoft_Naive_Bayes\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ Naive_Bayes está habilitado.  
  
 `Microsoft_Neural_Network\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Neural_Network está habilitado.  
  
 `Microsoft_Sequence_Clustering\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ Sequence_Clustering está habilitado.  
  
 `Microsoft_Time_Series\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Time_Series está habilitado.  
  
 `Microsoft_Linear_Regression\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Linear_Regression está habilitado.  
  
 `Microsoft_Logistic_Regression\ Enabled`  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Logistic_Regression está habilitado.  
  
> [!NOTE]  
>  Além das propriedades que definem os serviços mineração de dados disponíveis no servidor, há propriedades de mineração de dados que definem o comportamento de algoritmos específicos. Essas propriedades são configuradas quando você criar um modelo de mineração de dados individual, não ao nível do servidor. Para obter mais informações, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de Dados&#41;](../data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura física &#40;Analysis Services&#41;de mineração de dados](../data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurar propriedades do servidor no Analysis Services](server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
