---
title: Referências das coleções DataSources e DataSets (Construtor de Relatórios) | Microsoft Docs
description: Saiba mais sobre as coleções de fontes de dados e conjuntos de dados. Descubra como disponibilizá-los depois que o relatório for publicado em um servidor de relatório no Construtor de Relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8310d67c8305101b1729446d4d9e25bc463ea0fd
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681265"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>Coleções internas – referências de DataSources e DataSets (Construtor de Relatórios)
  A coleção **DataSources** representa todas as fontes de dados usadas em um relatório. De maneira semelhante, a coleção **DataSets** representa todos os conjuntos de dados para todas as fontes de dados em um relatório. Use o painel **Dados do Relatório** para obter uma exibição hierárquica dos conjuntos de dados do relatório organizados sob a fonte de dados a qual eles fazem referência. Se você incluir referências nessas coleções, não poderá ver os valores ao visualizar o relatório. Essas coleções estão disponíveis apenas após o relatório ter sido publicado em um servidor de relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 A coleção **DataSources** representa as fontes de dados referenciadas em uma definição de relatório publicada. É possível optar por incluir essas informações no relatório para documentar a origem dos dados do relatório. Essa coleção não está disponível no modo **Visualização** . A tabela a seguir descreve as variáveis dentro da coleção **DataSources** .  
  
|**Variável**|**Tipo**|**Descrição**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**Cadeia de caracteres**|O caminho completo da definição da fonte de dados no servidor de relatório. Por exemplo, você pode incluir uma lista de todas as fontes de dados que um relatório usou como parte de um histórico de relatório. O exemplo a seguir mostra o caminho completo da fonte de dados denominada AdventureWorks2012:<br /><br /> `/DataSources/AdventureWorks2012`.|  
|**Tipo**|**Cadeia de caracteres**|O tipo de provedor de dados para a fonte de dados. Por exemplo, `SQL`.|  
  
## <a name="datasets"></a>DataSets  
 A coleção **DataSets** representa os conjuntos de dados referenciados em uma definição de relatório. É possível optar por incluir a consulta no relatório em uma caixa de texto, de modo que um usuário interessado exatamente nos dados que estão no relatório possa ver o texto do comando original. Essa coleção não está disponível no modo **Visualização** . A tabela a seguir descreve os membros da coleção **DataSets** .  
  
|**Membro**|**Tipo**|**Descrição**|  
|----------------|--------------|---------------------|  
|**CommandText**|**Cadeia de caracteres**|Para fontes de dados do banco de dados, esta é a consulta usada para recuperar dados da fonte de dados. Se a consulta for uma expressão, essa será a expressão avaliada.|  
|**RewrittenCommandText**|**Cadeia de caracteres**|O valor de CommandText expandido do provedor de dados. Geralmente isso é usado para relatórios com parâmetros de consulta mapeados para parâmetros de relatório. O provedor de dados define essa propriedade ao expandir as referências do parâmetro do texto do comando nos valores constantes selecionados para os parâmetros de relatório mapeados.|  
  
### <a name="using-query-expressions"></a>Usando expressões de consulta  
 É possível usar expressões para definir a consulta contida em um conjunto de dados. É possível usar esse recurso para projetar relatórios em que a consulta é alterada com base na entrada do usuário, dos dados em outros conjuntos de dados ou outras variáveis. Para obter mais informações sobre consultas, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
