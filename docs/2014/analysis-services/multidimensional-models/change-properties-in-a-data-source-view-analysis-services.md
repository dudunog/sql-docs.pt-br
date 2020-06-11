---
title: Alterar propriedades em uma exibição da fonte de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- friendly names [Analysis Services]
- names [Analysis Services], data source views
- viewing tables
- displaying tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 4ccdabea-9c4d-460d-ba78-d23068143696
author: minewiskan
ms.author: owend
ms.openlocfilehash: 201ff28999efb006b80157125c85242d538d756a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537098"
---
# <a name="change-properties-in-a-data-source-view-analysis-services"></a>Alterar propriedades em uma exibição da fonte de dados (Analysis Services)
  Após definir uma exibição da fonte de dados usando o Assistente de Exibição da Fonte de Dados e adicionar tabelas, exibições, cálculos nomeados e consultas nomeadas à exibição da fonte de dados, convém alterar as propriedades relacionadas a:  
  
-   Critérios de correspondência da exibição da fonte de dados  
  
-   Opções avançadas de exibição da fonte de dados  
  
-   Nomes de objetos  
  
-   Metadados de objeto  
  
 Também é possível exibir os metadados de objeto recuperados a partir da fonte de dados que você não pode modificar.  
  
## <a name="viewing-or-changing-data-source-view-properties"></a>Exibindo ou alterando as propriedades da exibição da fonte de dados  
 As propriedades da exibição da fonte de dados, além de sua descrição, são configuradas pelo Assistente de Exibição da Fonte de Dados quando você define pela primeira vez a exibição da fonte de dados. A tabela a seguir lista e descreve as propriedades de uma exibição da fonte de dados.  
  
> [!NOTE]  
>  O painel Propriedades mostra as propriedades para o arquivo .dsv assim como o objeto DSV. Para exibir as propriedades do objeto, clique duas vezes nele no Gerenciador de Soluções. As Propriedades serão atualizadas para refletir as propriedades que você vê na tabela seguinte.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|fonte de dados|Especifica a fonte de dados da exibição da fonte de dados cujas propriedades você está exibindo.|  
|Description|Especifica a descrição da exibição da fonte de dados.|  
|Name|Especifica o nome da exibição da fonte de dados que aparece no Gerenciador de Soluções ou no banco de dados do Analysis Services. Você pode alterar o nome da exibição da fonte de dados aqui ou no Gerenciador de Soluções.|  
|NameMatchingCriteria|Os critérios de correspondência de nomes da fonte de dados. O padrão será (nenhum) se o Assistente de Exibição da Fonte de Dados detectar relações entre chave primária e chave estrangeira. Mesmo que essa propriedade tenha sido definida pelo Assistente de Exibição da Fonte de Dados, você poderá especificar um valor aqui. Se houver relações do banco de dados e você especificar um critério de correspondência de nomes, ambos serão usados para inferir relações entre as tabelas existentes e a tabela recém-adicionada.|  
|RetrieveRelationships|Especifica se as relações são recuperadas do banco de dados. O padrão é True.|  
|SchemaRestriction|Especifica as restrições, se houver alguma, dos esquemas recuperados de uma fonte de dados. Por padrão, não existe restrição de esquema.|  
  
## <a name="viewing-or-changing-datatable-properties"></a>Exibindo ou alterando as propriedades DataTable  
 As propriedades**DataTable** são as propriedades de tabelas, exibições e consultas nomeadas de uma exibição da fonte de dados. Elas são definidas quando algum desses objetos é adicionado à exibição da fonte de dados. A tabela a seguir lista e descreve as propriedades dos objetos **DataTable** de uma exibição da fonte de dados.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|AllowChangesDuringGeneration|Especifica se o Assistente de Geração de Esquema tem permissão para substituir uma tabela de exibição da fonte de dados durante a nova geração. Essa propriedade existirá apenas nas tabelas inicialmente geradas pelo Assistente de Geração de Esquema. Para obter mais informações, consulte [Noções básicas sobre geração incremental](understanding-incremental-generation.md).|  
|DataSource|Especifica a fonte de dados para o objeto. Não é possível editar essa propriedade.|  
|Description|Especifica a descrição da tabela, exibição ou consulta nomeada. Se a coluna ou exibição da fonte de dados do banco de dados subjacente tiver uma descrição armazenada como propriedade estendida, esse valor aparecerá. Você pode editar essa propriedade.|  
|FriendlyName|Especifica um nome para a tabela ou exibição mais fácil para os usuários entenderem ou mais relevante para a área de assunto. Por padrão, a propriedade **FriendlyName** de uma tabela ou exibição é igual à propriedade **Name** da tabela ou exibição. A propriedade **FriendlyName** é usada por objetos OLAP e de mineração de dados ao definir os nomes dos objetos com base nas tabelas ou exibições. Você pode editar essa propriedade.|  
|Name|Especifica o nome da tabela ou exibição subjacente ou o nome da consulta nomeada. A propriedade **Name** é usada por objetos OLAP e de mineração de dados ao definir nomes de objetos com base em consultas nomeadas. Essa propriedade é editável apenas no caso de consultas nomeadas.|  
|QueryDefinition|Especifica a definição de consulta nomeada. Essa propriedade aplica-se somente a consultas nomeadas e não pode ser editada diretamente. Para editá-la, edite a própria consulta nomeada.|  
|Esquema|Especifica o esquema de banco de dados válido para a tabela, exibição ou consulta nomeada. Essa propriedade não é editável.|  
|TableType|Especifica o tipo de tabela para a tabela, exibição ou consulta nomeada. Essa propriedade não é editável.|  
  
## <a name="viewing-or-changing-datacolumn-properties"></a>Exibindo ou alterando as propriedades DataColumn  
 As propriedades**DataColumn** são as propriedades das colunas em tabelas, exibições e consultas nomeadas de uma exibição da fonte de dados. Elas são definidas quando algum dos objetos a seguir é adicionado à exibição da fonte de dados, seja proveniente da tabela ou exibição subjacente, de uma consulta nomeada ou definido por um cálculo nomeado. A tabela a seguir lista e descreve as propriedades dos objetos **DataColumn** de uma exibição da fonte de dados.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|AllowNull|Especifica a propriedade de nulidade da coluna com base na coluna da tabela, no valor ou na consulta nomeada subjacente. Essa propriedade não é editável.|  
|Tipo de dados|Especifica o tipo de dados da coluna com base na coluna da tabela, no valor ou na consulta nomeada subjacente. Não é possível editar diretamente essa propriedade. No entanto, se for necessário alterar o tipo de dados de uma coluna de uma tabela ou exibição, substitua a tabela por uma consulta nomeada que converta a coluna para o tipo de dados desejado.|  
|DateTimeMode|Especifica o formato de serialização de data para as colunas **DateTime** . O valor padrão é **UnspecifiedLocal**. Essa propriedade pode ser editada.|  
|Description|Especifica a descrição da coluna. Se a coluna do banco de dados subjacente tiver uma descrição armazenada como propriedade estendida, esse valor aparecerá. Você pode editar essa propriedade.|  
|FriendlyName|Especifica o nome para a coluna de uma tabela ou exibição que seja mais fácil para os usuários entenderem ou mais relevante para a área de assunto. Por padrão, a propriedade **FriendlyName** da coluna de uma tabela ou exibição é igual à propriedade **Name** da coluna. A propriedade **FriendlyName** é usada por objetos OLAP e de mineração de dados ao definir atributos com base nas colunas de tabelas ou exibições. Você pode editar essa propriedade.|  
|Comprimento|Especifica o comprimento máximo da coluna com base nos dados da coluna da tabela ou exibição subjacente.|  
|Name|Especifica o nome da coluna subjacente ou o nome do cálculo nomeado. A propriedade **Name** é usada por objetos OLAP e de mineração de dados ao definir atributos com base em cálculos nomeados. Essa propriedade é editável apenas no caso de cálculos nomeados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Trabalhar com diagramas em um Designer de exibição da fonte de dados &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
