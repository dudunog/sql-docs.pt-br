---
description: Uso (DMX)
title: Uso (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e9108fc9bc53361a15d144f1f11afa62f9d5a97
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726037"
---
# <a name="usage-dmx"></a>Uso (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Ao usar o DMX (extensões de mineração de dados) para definir um novo modelo de Data Mining no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , você deve especificar como o algoritmo de Data Mining que cria o modelo usará cada coluna. Especifique as colunas como um dos tipos seguintes:  
  
-   **Key**  
  
-   **Key Sequence**  
  
-   **Key Time**  
  
-   **Prever**  
  
-   **PredictOnly**  
  
 As colunas deixadas sem-especificação em DMX são tratadas como colunas de entrada.  
  
 Para processar corretamente um modelo, o algoritmo precisará saber quais colunas são a coluna de chave que identifica exclusivamente cada uma das linhas; qual coluna é a coluna de destino para a criação de previsões, caso se esteja criando um modelo previsível, e quais colunas usar como colunas de entrada para criar relações que preveem a coluna de destino.  
  
 As colunas especificadas como o tipo de **previsão** são usadas como colunas de entrada e de saída. As colunas especificadas como **PredictOnly** são usadas apenas como colunas de saída. Os algoritmos específicos podem tratar as colunas Predict de forma diferente.  
  
 Para obter mais informações sobre os tipos de uso de coluna que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] suporta, consulte [colunas do modelo de mineração](/analysis-services/data-mining/mining-model-columns).  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
