---
title: Coleções internas em expressões (Construtor de Relatórios) | Microsoft Docs
description: Descubra coleções internas em expressões para fazer referência a coleções como parâmetros, campos e conjuntos de dados em seus relatórios no Construtor de Relatórios.
ms.date: 3/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5dbc7cf2683f78118087d18b2dd51865bf52f3d
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84880267"
---
# <a name="built-in-collections-in-expressions-report-builder"></a>Coleções internas em expressões (Construtor de Relatórios)
  Em uma expressão em um relatório, você pode incluir referências às seguintes coleções internas: ReportItems, Parâmetros, Campos, DataSets, DataSources, Variáveis e campos internos para informações globais, como o nome do relatório. Nem todas as coleções são exibidas na caixa de diálogo **Expressão** . As coleções de DataSets e DataSources estão disponíveis apenas em tempo de execução para relatórios publicados em um servidor de relatório. A coleção de ReportItems é uma coleção de caixas de texto em uma região do relatório, por exemplo, as caixas de texto em uma página ou em um cabeçalho de página.  
  
 Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-built-in-collections"></a><a name="Collections"></a> Entendendo as coleções internas  
 A tabela a seguir lista as coleções internas disponíveis quando você escreve uma expressão. Cada linha inclui o nome programático que diferencia maiúsculas de minúsculas para a coleção, você puder usar a caixa de diálogo Expressão para adicionar uma referência interativamente à coleção, um exemplo e uma descrição que inclui quando os valores da coleção são inicializados e estão disponíveis para uso.  
  
|Coleção interna|Categoria na caixa de diálogo Expressão|Exemplo|Descrição|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**Variáveis globais**|Campos internos|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|Representa variáveis globais úteis para relatórios, como o nome do relatório ou o número da página. Sempre disponível.<br /><br /> Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Usuário**|Campos internos|`=User.UserID`<br /><br /> - ou -<br /><br /> `=User.Language`|Representa uma coleção de dados sobre o usuário que executa o relatório, como a configuração de idioma ou a ID de usuário. Sempre disponível.<br /><br /> Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Parâmetros**|Parâmetros|`=Parameters("ReportMonth").Value`<br /><br /> - ou -<br /><br /> `=Parameters!ReportYear.Value`|Representa a coleção de parâmetros do relatório, cada um dos quais pode ter um valor único ou vários valores. Não disponível até que a inicialização do processamento seja executada. Para obter mais informações, consulte [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).|  
|**Campos(** *\<Dataset>* **)**|Campos|`=Fields!Sales.Value`|Representa a coleção de campos do conjunto de dados disponível para o relatório. Disponível depois que os dados são recuperados de uma fonte de dados em um conjunto de dados. Para obter mais informações, consulte [Referências de coleções de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).|  
|**Conjuntos de Dados**|Não exibido|`=DataSets("TopEmployees").CommandText`|Representa a coleção de conjuntos de dados referidos no corpo de uma definição de relatório. Não inclui fontes de dados usadas apenas em cabeçalhos ou rodapés de páginas. Não disponível em visualização local. Para obter mais informações, consulte [Referências de coleções DataSources e DataSets &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**DataSources**|Não exibido|`=DataSources("AdventureWorks2012").Type`|Representa a coleção de fontes de dados referidas de dentro do corpo de um relatório. Não inclui fontes de dados usadas apenas em cabeçalhos ou rodapés de páginas. Não disponível em visualização local. Para obter mais informações, consulte [Referências de coleções DataSources e DataSets &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**Variáveis**|`Variables`|`=Variables!CustomTimeStamp.Value`|Representa a coleção de variáveis de relatório e variáveis de grupo. Para obter mais informações, consulte [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md).|  
|**ReportItems**|Não exibido|`=ReportItems("Textbox1").Value`|Representa a coleção de caixas de texto para um item de relatório. Essa coleção pode ser usada para resumir itens na página para inclusão em um cabeçalho ou rodapé de página. Para obter mais informações, consulte [Referências de coleções ReportItems &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md).|  
  
##  <a name="using-collection-syntax-in-an-expression"></a><a name="Syntax"></a> Usando sintaxe de coleção em uma expressão  
 Para fazer referência a uma coleção em uma expressão, use a sintaxe padrão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para um item em uma coleção. A tabela a seguir mostra exemplos de sintaxe de coleção.  
  
|Sintaxe|Exemplo|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar uma expressão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
