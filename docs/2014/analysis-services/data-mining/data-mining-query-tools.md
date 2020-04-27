---
title: Interfaces de consulta de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c59d3a18c1fd36f82e8ea60e42d1b9f6e2f34c2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084977"
---
# <a name="data-mining-query-interfaces"></a>Interfaces de Consulta de Mineração de Dados
  Consultas de mineração de dados são baseadas na linguagem DMX. Você usa DMX para todas as tarefas de previsão e modelagem, inclusive classificação, análise de risco, geração de recomendações e regressão linear. Você também pode recuperar os padrões e as estatísticas que foram geradas quando processou o modelo.  
  
 A sintaxe para uma consulta de previsão que usa DMX é semelhante à sintaxe para uma consulta em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Tanto o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quanto o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornecem ferramentas que o ajudam a criar consultas de previsão em DMX.  
  
 Este tópico descreve as interfaces que você pode usar para criar e executar consultas de mineração de dados usando DMX.  
  
 [Ferramentas de consulta](#bkmk_Tools)  
  
-   [Construtor de Consultas de previsão](#bkmk_Builder)  
  
-   [Editor de consultas](#bkmk_QueryEditor)  
  
-   [Modelos DMX](#bkmk_Templates)  
  
-   [Serviços de Integração](#bkmk_SSIS)  
  
 [Interfaces de programação de aplicativo](#bkmk_API)  
  
##  <a name="data-mining-query-tools"></a><a name="bkmk_Tools"></a>Ferramentas de consulta de mineração de dados  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece as seguintes ferramentas que podem ser usadas para criar consultas de previsão, consultas de conteúdo e consultas de definição de dados em objetos de mineração de dados:  
  
-   Construtor de Consultas de Previsão  
  
-   Editor de Consultas  
  
-   Modelos DMX  
  
-   Componentes de mineração de dados do Integration Services  
  
###  <a name="prediction-query-builder"></a><a name="bkmk_Builder"></a> Construtor de Consultas de Previsão  
 O Construtor de Consultas de Previsão está incluído na guia **Previsão do Modelo de Mineração** do Designer de Data Mining, que esta disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você utiliza o construtor de consultas, é possível usar ferramentas gráficas para selecionar um modelo de mineração, adicionar novo caso de dados e funções de predição. O Construtor de Consultas de previsão inclui um editor de texto que você pode usar para modificar a consulta manualmente e um painel de **resultados** simples para exibir os resultados da consulta.  
  
###  <a name="query-editor"></a><a name="bkmk_QueryEditor"></a> Editor de Consultas  
 O editor de consultas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no fornece ferramentas que você pode usar para compilar e executar consultas DMX. É possível conectar-se a uma instância do SQL Server Analysis Services e, em seguida, selecionar um banco de dados, colunas de estrutura de mineração e um modelo de mineração. O **Gerenciador de Metadados** contém uma lista de funções de previsão que você pode procurar.  
  
###  <a name="dmx-templates"></a><a name="bkmk_Templates"></a> Modelos DMX  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece modelos de consulta interativa DMX que você poderá usar para criar consultas DMX. Se você não vir a lista de modelos, clique em **Exibição** na barra de ferramentas e selecione **Explorador de Modelos**. Para ver todos os modelos do Analysis Services, incluindo modelos para DMX, MDX e XMLA, clique no ícone do cubo.  
  
 Para criar uma consulta usando um modelo, você pode arrastar o modelo em uma janela de consulta aberta ou pode clicar duas vezes no modelo para abrir uma nova conexão e um novo painel de consulta.  
  
 Para ver um exemplo de como criar uma consulta de previsão com base em um modelo, consulte [Criar uma consulta de previsão Singleton com base em um modelo](create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  O Suplemento de Mineração de Dados para o Microsoft Office Excel também contém vários modelos, junto com um construtor de consultas interativo que pode ajudá-lo a compor instruções DMX complexas. Para usar os modelos, clique em **Consulta**e **Avançado** no Cliente de Mineração de Dados.  
  
###  <a name="integration-services-data-mining-components"></a><a name="bkmk_SSIS"></a>Integration Services componentes de mineração de dados  
 Você também pode incluir consultas de previsão como parte de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacote. As tarefas e transformações no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a seguir fornecem suporte para a criação e execução de consultas de previsão de DMX e instruções DMX.  
  
|Componente|Descrição|  
|---------------|-----------------|  
|Tarefa Consulta de Mineração de dados|Executa consultas DMX e outras instruções DMX como parte de um fluxo de controle.<br /><br /> O editor de tarefa fornece o Construtor de Consulta de Previsão e uma caixa de texto para modificar a consulta DMX manualmente. Porém, o editor de tarefa não pode validar a consulta em objetos em uma solução do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Portanto, é melhor criar uma consulta dentro do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e, em seguida, colar o texto da instrução ou consulta no editor de tarefa.|  
|Transformação Consulta de Mineração de Dados|Executa uma consulta de previsão dentro de um fluxo de dados, usando os dados fornecidos por uma fonte de fluxo de dados.<br /><br /> O editor de tarefa fornece o Construtor de Consulta de Previsão e uma caixa de texto para modificar a consulta DMX manualmente.<br /><br /> A transformação somente pode ser usada para criar consultas que usam dados no fluxo de dados; ou seja, consultas que usam a sintaxe PREDICTION JOIN. Este componente não pode ser usado para executar consultas de conteúdo ou outros tipos de instruções DMX.|  
  
##  <a name="application-programming-interfaces"></a><a name="bkmk_API"></a>Interfaces de programação de aplicativo  
 Você pode criar aplicativos personalizados que executam consultas em relação a modelos de mineração de dados usando uma variedade de linguagens de programação, em combinação com protocolos de servidor como OLE DB ou cliente ADOMD do Analysis Services. Para obter mais informações, consulte [Programação de Data Mining](../dev-guide/data-mining-programming.md).  
  
 Porém, o XMLA constitui o formato de mensagem subjacente para todas as interações com um servidor do Analysis Service. Dentro de uma mensagem de XMLA, as consultas são representadas de maneira diferente dependendo se você está enviando uma consulta de previsão com base em DMX, uma consulta de conteúdo ou uma consulta que recupera metadados modelo usando os conjuntos de linhas de esquema de mineração de dados.  
  
-   O texto de **consultas de previsão** (e todas as outras instruções DMX) é enviado em XMLA usando o método [Método Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), com a consulta DMX colocada como texto dentro do [Elemento Statement &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) do elemento [Elemento Command &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Para recuperar o **conteúdo modelo** e os **metadados modelo**, como o número de clusters, os atributos usados em árvores de decisão, a data de processamento do modelo e os parâmetros de algoritmo usados ao criar o modelo, você pode usar o método [Método Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) e especificar um dos conjuntos de linhas de esquema de mineração de dados no cabeçalho [Elemento RequestType &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla). Para restringir o escopo da consulta, insira critérios como restrições dentro do elemento [Elemento RestrictionList &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Soluções de mineração de dados](data-mining-solutions.md)   
 [Compreendendo a instrução DMX SELECT](/sql/dmx/understanding-the-dmx-select-statement)   
 [Estrutura e uso de consultas de previsão DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Criar uma consulta DMX no SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
