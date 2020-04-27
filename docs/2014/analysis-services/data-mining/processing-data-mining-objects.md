---
title: Processando objetos de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- processing objects [Analysis Services]
- mining structures [Analysis Services]
- process [Analysis Services]
- mining structures [Analysis Services], creating
- mining structures [Analysis Services], how-to topics
- mining structures [Analysis Services], processing
ms.assetid: 0f6993c0-0917-4935-82f9-7b8a8a7cc627
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65c61f6e4b571880b6607bb647d2629a3b6864f7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083146"
---
# <a name="processing-data-mining-objects"></a>Processando objetos de mineração de dados
  Um objeto de mineração de dados é apenas um contêiner vazio até que seja processado. O*processamento* de um modelo de mineração de dados também é chamado de *treinamento*.  
  
 **Processando estruturas de mineração:** uma estrutura de mineração obtém dados de uma fonte de dados externa, conforme definido pelas associações de coluna e pelos metadados de uso, e lê esses dados. Esses dados são totalmente lidos e, depois, analisados para se extrair diversas estatísticas. O Analysis Services armazena uma representação compacta de dados, que é adequada para a análise de algoritmos de mineração de dados, em um cache local. Você pode tanto manter esse cache com excluí-lo depois do processamento de seus modelos. Por padrão, o cache é armazenado. Para obter mais informações, consulte [Processar uma estrutura de mineração](process-a-mining-structure.md).  
  
 **Processando modelos de mineração:** um modelo de mineração está vazio e contém apenas definições até que seja processado. Para processar um modelo de mineração, a estrutura de mineração na qual ele se baseia deve ter sido processada. O modelo de mineração obtém dados do cache da estrutura de mineração e aplica quaisquer filtros que tenham sido criados no modelo. Em seguida, ele submete o conjunto de dados ao algoritmo para detectar padrões. Depois que o modelo é processado, ele armazena apenas os resultados do processamento, e não os próprios dados. Para obter mais informações, consulte [Processar um modelo de mineração](process-a-mining-model.md).  
  
 O diagrama a seguir mostra o fluxo de dados quando uma estrutura de mineração é processada e quando um modelo de mineração é processado.  
  
 ![Processamento de dados: origem para estrutura para modelo](../media/dmcon-modelarch.gif "Processamento de dados: origem para estrutura para modelo")  
  
## <a name="viewing-the-results-of-processing"></a>Exibindo os resultados do processamento  
 Após o processamento de uma estrutura de mineração, ela conterá uma representação compacta dos dados para uso em análises estatísticas. Se o cache não foi limpo, você poderá acessar os dados dos seguintes modos:  
  
-   Criando uma consulta DMX (Data Mining Extensions) no modelo e detalhando a estrutura. Para obter mais informações, consulte [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
-   Procurando um modelo com base na estrutura e usando uma das opções da interface do usuário para detalhar os casos na estrutura. Para obter mais informações, consulte [Visualizadores de Modelo de Mineração de Dados](data-mining-model-viewers.md)ou [Detalhar dados de caso com base em um modelo de mineração](drill-through-to-case-data-from-a-mining-model.md).  
  
-   Criando uma consulta DMX nos casos da estrutura. Para obter mais informações, consulte [SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases).  
  
 Após o processamento de um modelo de mineração, ele contém apenas os padrões derivados da análise e os mapeamento dos resultados do modelo com relação aos dados de treinamento armazenados em cache. Você poderá procurar ou consultar os resultados do modelo, chamados de *conteúdo do modelo*, ou consultar os casos da estrutura e do modelo se eles tiverem sido armazenados em cache.  
  
 O conteúdo de cada modelo de mineração depende do algoritmo que foi usado para criá-lo. Por exemplo, se você tiver um modelo de clustering e um modelo de árvores de decisão, o conteúdo deles será muito diferente, mesmo que tenham usado exatamente os mesmos dados. Para obter mais informações, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="processing-requirements"></a>Requisitos de processamento  
 Os requisitos de processamento variam de acordo com a base dos modelos de mineração: apenas dados relacionais ou uma fonte de dados multidimensional.  
  
 Na fonte de dados relacional, o processamento exige apenas a criação de dados de treinamento e a execução de algoritmos de mineração nesses dados. Entretanto, modelos de mineração baseados em objetos OLAP, como dimensões e medidas, exigem que os dados subjacentes estejam em um estado processado. Isso pode exigir que os objetos multidimensionais sejam processados para popular o modelo de mineração.  
  
 Para obter mais informações, consulte [Requisitos e considerações sobre processamento &#40;Mineração de dados&#41;](processing-requirements-and-considerations-data-mining.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)   
 [Estruturas de mineração &#40;Analysis Services de mineração de dados&#41;](mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services de mineração de dados&#41;](mining-models-analysis-services-data-mining.md)   
 [Arquitetura lógica &#40;Analysis Services – Mineração de dados&#41;](logical-architecture-analysis-services-data-mining.md)  
  
  
