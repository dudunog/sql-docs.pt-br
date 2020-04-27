---
title: Propriedades de fluxo de dados que podem ser definidas usando expressões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70a956834108c21dd7b17bb9f3e04db38f29bfa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059937"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>Propriedades de fluxo de dados que podem ser definidas usando expressões
  Os valores de certas propriedades dos objetos de fluxo de dados podem ser especificados usando expressões de propriedades disponíveis no contêiner da tarefa de Fluxo de Dados.  
  
 Para obter informações sobre como usar expressões de propriedade, consulte [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md).  
  
 É possível usar expressões de propriedade para personalizar configurações para cada instância implantada de um pacote. Você também pode usar expressões de propriedades para especificar restrições de tempo de execução para um pacote, usando a opção **/set** com o utilitário de prompt de comando **dtexec** . Por exemplo, você pode restringir o `MaximumThreads` usado pela transformação Classificação ou o `MaxMemoryUsage` das transformações Agrupamento Difuso e Pesquisa Difusa. Se irrestritas, essas transformações podem armazenar em cache grandes quantias de dados na memória.  
  
 Para especificar uma expressão de propriedade para uma das propriedades de objetos de fluxo de dados listadas nesse tópico, exiba a janela **Propriedades** para a tarefa de Fluxo de Dados selecionando a tarefa de Fluxo de Dados na superfície **Fluxo de Controle** do designer, ou selecionando a guia **Fluxo de Dados** do designer sem selecionar nenhum componente individual ou caminho. Selecione a propriedade **Expressões** e clique nas reticências (...) para exibir a caixa de diálogo **Editor de Expressões de Propriedades** . Abra a lista suspensa **Propriedade** para selecionar uma propriedade e digite uma expressão na caixa de texto **Expressão** ou clique nas reticências (...) para exibir a caixa de diálogo **Construtor de Expressões** .  
  
 A lista **Propriedade** exibe as propriedades disponíveis para apenas esses objetos de fluxo de dados já colocados na superfície **Fluxo de Dados** do designer. Portanto, não é possível usar a lista **Propriedade** para exibir todas as possíveis propriedades de objetos de fluxo de dados que aceitam expressões de propriedades. Por exemplo, se você colocou uma origem do ADO NET na superfície do designer, a lista de **Propriedades** conterá uma entrada `[ADO NET Source].[SqlCommand]` para a propriedade. A lista também exibe muitas propriedades da própria tarefa de Fluxo de Dados.  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>Propriedades de objetos de fluxo de dados que aceitam expressões de propriedade  
 Os valores das propriedades na lista a seguir podem ser especificados usando expressões de propriedades.  
  
### <a name="data-flow-sources"></a>Origens do Fluxo de Dados  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Origem do ADO NET|Propriedade TableOrViewName<br /><br /> Propriedade SqlCommand|  
|Origem XML|Propriedade XMLData<br /><br /> Propriedade XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Transformações de Fluxo de Dados  
 Para obter mais informações sobre essas propriedades personalizadas, consulte [Propriedades Personalizadas de Transformação](data-flow/transformations/transformation-custom-properties.md).  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Transformação Divisão Condicional|Propriedade FriendlyExpression|  
|transformação Coluna Derivada|Propriedade FriendlyExpression|  
|transformação Agrupamento Difuso|Propriedade MaxMemoryUsage|  
|transformação Pesquisa Difusa|Propriedade MaxMemoryUsage|  
|transformação Pesquisa|Propriedade SqlCommand<br /><br /> Propriedade SqlCommandParam|  
|transformação Comando OLE DB|Propriedade SqlCommand|  
|transformação Amostragem Percentual|Propriedade SamplingValue|  
|transformação Dinâmica|Propriedade PivotKeyValue|  
|Transformação Amostragem de Linhas|Propriedade SamplingValue|  
|Transformação Classificação|Propriedade MaximumThreads|  
|Transformação Não Dinâmica|Propriedade PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinos de Fluxo de Dados  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Destino do ADO NET|Propriedade TableOrViewName<br /><br /> Propriedade BatchSize<br /><br /> Propriedade CommandTimeout|  
|Destino de arquivo simples|Propriedade Header|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Destino Compact|Propriedade TableName|  
|Destino [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Propriedade BulkInsertTableName<br /><br /> Propriedade BulkInsertFirstRow<br /><br /> Propriedade BulkInsertLastRow<br /><br /> Propriedade BulkInsertOrder<br /><br /> Propriedade Timeout|  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet), em pragmaticworks.com  
  
## <a name="see-also"></a>Consulte Também  
 [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md)   
 [Propriedades comuns](../../2014/integration-services/common-properties.md)   
 [Propriedades personalizadas da transformação](data-flow/transformations/transformation-custom-properties.md)   
 [Propriedades do caminho](../../2014/integration-services/path-properties.md)  
  
  
