---
title: Guia discriminação de atributo (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7e8d9593cd45ec5a92ea07051fe424698d8ece6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66063128"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>Guia Distinção de Atributo (Visualizador do Modelo de Mineração)
  Utilize a guia **Distinção de Atributo** para comparar os estados dos atributos de entrada e ver como eles estão relacionados aos atributos de saída. Os valores de atributo que compõem a maior diferença entre os dois estados de atributos previsíveis são listados em primeiro lugar.  
  
 **Para obter mais informações:** [Algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm.md), [Procurar um modelo usando o Visualizador Naive Bayes da Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração é aberto automaticamente no visualizador personalizado correto.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Para cada modelo, você pode escolher um visualizador personalizado ou o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver.  
  
 **Atributo**  
 Escolha um atributo previsível.  
  
 **Valor 1**  
 Escolha um estado do atributo previsível a ser comparado com a condição que está contida em **Valor 2**.  
  
 **Valor 2**  
 Selecione o estado do atributo previsível a ser comparado com o estado que está contido em **Valor 1**. Você também pode selecionar **todos os outros Estados** para comparar o valor no **valor 1** com seu complemento – ou seja, todos os outros valores, exceto o valor 1.  
  
 **Pontuações de \<discriminação para valor 1 \<> e valor 2>**  
 O gráfico contém as seguintes colunas, que descrevem como o atributo de destino está relacionado aos estados específicos do atributo de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Atributos**|Um atributo de entrada no modelo de mineração.|  
|**Valores**|Um estado do atributo listado em **Atributos**.|  
|**Favorece \<o valor 1>**|A barra indica se o atributo atual e valor favorecem o resultado de destino selecionado em **Valor 1**.|  
|**Favorece \<o valor 2>**|A barra indica se o atributo atual e valor favorecem o resultado de destino selecionado em **Valor 2**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
