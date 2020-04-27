---
title: Algoritmos de mineração de dados (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0bf6c0c1126dff29107636e0956d92d4b314a7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086506"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>Algoritmos de mineração de dados (Suplementos de mineração de dados do SQL Server)
  Os Suplementos de Mineração de Dados para Office oferecem suporte à criação de modelos analíticos usando os algoritmos de mineração de dados a seguir. Todos os algoritmos são baseados nos métodos de aprendizado automatizado conhecido e foram implementados pelo Microsoft Research.  
  
## <a name="algorithms"></a>Algoritmos  
  
|Método de aprendizado automatizado|Como ele funciona|  
|-----------------------------|------------------|  
|Algoritmo de Regras de Associação da Microsoft|Descobrir quais produtos são comprados juntos ou quais eventos ocorrem juntos, e usar o modelo para criar recomendações.<br /><br /> [https://msdn.microsoft.com/library/ms174916.aspx](https://msdn.microsoft.com/library/ms174916.aspx)|  
|Algoritmo Microsoft Clustering|Definir segmentos de mercado, agrupar automaticamente clientes relacionados, ou localizar relações nos dados para usar em mineração adicional.<br /><br /> [https://msdn.microsoft.com/library/ms174879.aspx](https://msdn.microsoft.com/library/ms174879.aspx)|  
|Algoritmo Árvores de Decisão da Microsoft|Identificar relações anteriormente desconhecidas entre vários elementos dos dados para informar melhor suas decisões, ou localizar os fatores que levam a resultados específicos.<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
|Algoritmo Regressão Linear da Microsoft|Localizar uma fórmula matemática que descreva fatores que contribuem para um resultado numérico.<br /><br /> [https://msdn.microsoft.com/library/ms174824.aspx](https://msdn.microsoft.com/library/ms174824.aspx)|  
|Algoritmo Regressão Logística da Microsoft|Identificar os fatores que contribuem para os resultados binários, além de saber como usar isso para afetar os resultados.<br /><br /> [https://msdn.microsoft.com/library/ms174828.aspx](https://msdn.microsoft.com/library/ms174828.aspx)|  
|Algoritmo Microsoft Naïve Bayes|Explorar as relações nos seus dados e localizar aquelas mais associadas a um resultado.<br /><br /> [https://msdn.microsoft.com/library/ms174806.aspx](https://msdn.microsoft.com/library/ms174806.aspx)|  
|Algoritmo Redes Neurais da Microsoft|Localizar relações ocultas entre várias entradas e até mesmo saídas. Usar para exploração ou para previsão.<br /><br /> [https://msdn.microsoft.com/library/ms174941.aspx](https://msdn.microsoft.com/library/ms174941.aspx)|  
|Algoritmo Microsoft Time Series|Usar dados históricos para prever valores futuros.<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>Opções avançadas  
 Quando usa o Cliente de Mineração de Dados para Excel, você tem a opção de criar seus próprios modelos e estruturas de mineração de dados, ou de ajustar os parâmetros dos algoritmos.  
  
 [Parâmetros de algoritmo &#40;SQL Server suplementos de mineração de dados&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 Há duas maneiras de personalizar seus modelos usando essas opções avançadas:  
  
-   Use o assistente de **consulta de mineração de dados** para criar seu modelo.  
  
-   No **cliente de mineração de dados**, depois de iniciar o assistente, clique em **parâmetros**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de consulta SQL Server suplementos de mineração de dados&#41;](query-sql-server-data-mining-add-ins.md)   
 [Modelagem avançada &#40;suplementos de mineração de dados para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  
