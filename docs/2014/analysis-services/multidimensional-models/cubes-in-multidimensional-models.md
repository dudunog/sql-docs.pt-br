---
title: Cubos em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
author: minewiskan
ms.author: owend
ms.openlocfilehash: ab1051981ddcac948a447e814c278fab4fb61496
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547196"
---
# <a name="cubes-in-multidimensional-models"></a>Cubos em modelos multidimensionais
  Um cubo é uma estrutura multidimensional que contém informações para fins analíticos; os principais elementos constituintes de um cubo são dimensões e medidas. As dimensões definem a estrutura do cubo que você usa para fazer divisões, e as medidas fornecem valores numéricos agregados de interesse do usuário final. Como é uma estrutura lógica, um cubo permite a um aplicativo cliente recuperar valores, de medidas, como se estivessem contidos em células no cubo; as células são definidas para cada valor resumido possível. Uma célula, no cubo, é definida pela interseção de membros de dimensão e contém os valores agregados das medidas nessa interseção específica.  
  
## <a name="benefits-of-using-cubes"></a>Benefícios do uso de cubos  
 Um cubo oferece um único local onde todos os dados relacionados são armazenados para análise.  
  
## <a name="components-of-cubes"></a>Componentes de cubos  
 Um cubo é constituído de:  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Dimensões|[Dimensões em modelos multidimensionais](dimensions-in-multidimensional-models.md)|  
|Medidas e Grupos de Medidas|[Criar medidas e grupos de medidas em modelos multidimensionais](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Partições|[Partições em modelos multidimensionais](partitions-in-multidimensional-models.md)|  
|Perspectivas|[Perspectivas em modelos multidimensionais](perspectives-in-multidimensional-models.md)|  
|Hierarquias|[Criar hierarquias definidas pelo usuário](user-defined-hierarchies-create.md)|  
|Ações|[Ações em modelos multidimensionais](actions-in-multidimensional-models.md)|  
|KPI (indicadores de desempenho chave)|[Indicadores Chave de Desempenho &#40;KPIs&#41; em Modelos Multidimensionais](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Cálculos|[Cálculos em modelos multidimensionais](calculations-in-multidimensional-models.md)|  
|Translations|[Traduções em modelos multidimensionais](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criar um cubo usando o Assistente para Cubos](create-a-cube-using-the-cube-wizard.md)|Descreve como usar o Assistente para Cubos para definir um cubo, as dimensões, os atributos de dimensão e as hierarquias definidas pelo usuário.|  
|[Criar medidas e grupos de medidas em modelos multidimensionais](create-measures-and-measure-groups-in-multidimensional-models.md)|Descreve como definir os grupos de medidas.|  
|[Cálculos em modelos multidimensionais](calculations-in-multidimensional-models.md)|Descreve como definir e configurar um cálculo em um script MDX.|  
|[Ações em modelos multidimensionais](actions-in-multidimensional-models.md)|Descreve como definir e configurar uma ação.|  
|[Perspectivas em modelos multidimensionais](perspectives-in-multidimensional-models.md)|Descreve como definir e configurar uma perspectiva.|  
|[Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Descreve como trabalhar com procedimentos armazenados.|  
  
  
