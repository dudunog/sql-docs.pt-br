---
title: Medidas (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1ca545e081826f1b81117e377f370136a7b4998
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067006"
---
# <a name="measures-ssas-tabular"></a>Medidas (SSAS tabular)
  Em modelos de tabela, uma medida é um cálculo criado usando uma fórmula DAX para uso em um cliente de relatório. As medidas são avaliadas com base em campos, filtros e usuários de segmentações de dados selecionados no aplicativo cliente de relatório.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_understanding)  
  
-   [Definindo medidas usando a grade de medida](#bkmk_def_mg)  
  
-   [Propriedades das medidas](#bkmk_properties)  
  
-   [Usando uma medida em um KPI](#bkmk_KPI)  
  
-   [Tarefas relacionadas](#bkmk_rel_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_understanding"></a>Benefícios  
 As medidas podem se basear em funções de agregação padrão, como AVERAGE, COUNT ou SUM, ou é possível definir sua própria fórmula usando-se o DAX. Além da fórmula, cada medida tem propriedades, definidas pelo tipo de dados de medida, como Nome, Detalhe da Tabela, Formato e Casas Decimais.  
  
 Quando as medidas foram definidas em um modelo, os usuários podem acrescentá-los a um relatório ou Tabela Dinâmica. Dependendo das perspectivas e das funções, as medidas aparecem na Lista de Campos com a tabela associada, e estão disponíveis para todos os usuários do modelo. As medidas são geralmente criadas na tabela de fatos; no entanto, as medidas podem ser independentes da tabela com a qual estão associadas.  
  
 É importante entender as diferenças fundamentais entre uma coluna calculada e uma medida. Em uma coluna calculada, uma fórmula é avaliada como um valor para cada linha na coluna. Por exemplo, em uma tabela FactSales, uma coluna calculada chamada TotalProfit com a fórmula a seguir calcula um valor para o lucro total para cada linha (uma linha por venda) na tabela FactSales:  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 A coluna calculada TotalProfit pode então ser usada em um cliente de relatório assim como qualquer outra coluna.  
  
 Uma medida, por outro lado, é avaliada como um valor com base em uma seleção de usuário; um contexto de filtro definido em uma Tabela Dinâmica ou relatório. Por exemplo, uma medida na tabela FactSales é criada com a seguinte fórmula:  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 Um analista de vendas, usando o Excel, que saber o lucro total para uma categoria de produtos. Cada categoria de produto é composta por vários produtos. O analista de vendas seleciona a coluna ProductCategoryName e a adiciona à janela de filtro de Rótulos de linha de uma Tabela Dinâmica; uma linha para cada categoria de produto é então exibida na Tabela Dinâmica. O usuário em seguida seleciona a medida Soma de TotalProfit. Uma medida será acrescentada por padrão à janela de filtro Valores. A medida calcula a soma de lucro total e exibe os resultados para cada categoria de produto. O analista de vendas pode então filtrar a soma de lucro total para cada categoria de produto usando uma segmentação de dados, por exemplo, adicionando CalendarYear como uma segmentação de dados para exibir a soma de lucro total para cada categoria de produto por ano.  
  
|ProductCategoryName|Soma de TotalProfit|  
|-------------------------|------------------------|  
|Áudio|$2,731,061,308.69|  
|Câmeras e filmadoras|$620,623,675.75|  
|Computadores|$392,999,044.59|  
|Tv e Vídeo|$946,989,702.51|  
|**Grand Total**|**$4,691,673,731.53**|  
  
##  <a name="defining-measures-by-using-the-measure-grid"></a><a name="bkmk_def_mg"></a>Definindo medidas usando a grade de medida  
 As medidas são criadas em tempo de design usando a grade de medida no designer de modelo. Cada tabela tem uma grade de medida. Por padrão, a grade de medida é exibida abaixo de cada tabela no designer de modelos. Você também pode escolher não exibir a grade de medida para uma tabela específica. Para alternar a exibição da grade de medida de uma tabela, clique no menu **tabela** e, em seguida, clique em **Mostrar grade de medida**.  
  
 Na grade de medida, você pode criar medidas das seguintes maneiras:  
  
-   Clique em uma célula vazia na grade de medida, e digite uma fórmula DAX na barra de fórmulas. Quando você clicar em ENTER para completar a fórmula, a medida será exibida na célula na grade de medida.  
  
-   Crie uma medida usando uma função de agregação padrão clicando em uma coluna, clicando no botão AutoSoma (∑) na barra de ferramentas e clicando em uma função de agregação padrão. Agregações padrão são: Sum, Average, Count, DistinctCount, Max, Min. As medidas criadas usando o botão AutoSoma sempre serão exibidas diretamente na grade de medida embaixo da coluna.  
  
 Por padrão, ao usar AutoSoma, o nome da medida é definido pelo nome da coluna associada seguido por dois-pontos e pela fórmula. O nome pode ser alterado na barra de fórmula ou na configuração de propriedade **Nome da Medida** na janela Propriedades. Ao criar uma medida usando uma fórmula personalizada, você pode digitar um nome na barra de fórmula, seguido por dois-pontos e pela fórmula, ou pode digitar um nome na configuração de propriedade **Nome da Medida** na janela de Propriedades.  
  
 É importante nomear medidas com cuidado. O nome de medida será exibido com a tabela associada na Lista de Campos do cliente de relatório. Um KPI também será nomeado de acordo com a medida de base. Uma medida não pode ter o mesmo nome de qualquer coluna em qualquer tabela no modelo.  
  
> [!TIP]  
>  É possível agrupar medidas de várias tabelas em uma tabela. Para tanto, crie uma tabela vazia e, depois, mova ou crie novas medidas nela. Lembre-se de que talvez seja necessário incluir nomes de tabelas em fórmulas DAX ao referenciar colunas em outras tabelas.  
  
 Se as perspectivas tiverem sido definidas para o modelo, as medidas não serão acrescentadas automaticamente a essas perspectivas. Você deve acrescentar medidas manualmente a uma perspectiva usando a caixa de diálogo Perspectivas. Para obter mais informações, consulte [Perspectivas &#40;SSAS de Tabela&#41;](perspectives-ssas-tabular.md).  
  
##  <a name="measure-properties"></a><a name="bkmk_properties"></a>Propriedades da medida  
 Cada medida tem propriedades que definem isto. As propriedades de medidas, junto com as propriedades de colunas associadas podem ser editadas na janela Propriedades. As medidas têm as seguintes propriedades:  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Descrição**|Em branco|Descrição da medida. A descrição não aparecerá com a medida em um cliente de relatório.|  
|**Ao**|Automaticamente determinado do tipo de dados da coluna referenciado na expressão de fórmula.|Formato da medida. Por exemplo, moeda ou percentual.|  
|**Fórmula**|A fórmula inserida na barra de fórmula quando a medida foi criada.|A fórmula da medida.|  
|**Nome da Medida**|Se AutoSoma for usado, o nome da medida precederá o nome da coluna seguido por dois-pontos. Se uma fórmula personalizada for inserida, digite um nome seguido por dois-pontos e digite a fórmula.|O nome da medida conforme é exibida em uma Lista de Campo do cliente de relatório.|  
  
##  <a name="using-a-measure-in-a-kpi"></a><a name="bkmk_KPI"></a>Usando uma medida em um KPI  
 Um KPI (Indicador Chave de Desempenho) é definido por um valor *Base* , definido por uma medida, em relação a um valor de *Destino* , também definido por uma medida ou valor absoluto. Um KPI também inclui *Status*, um cálculo onde o valor Base é avaliado em relação ao valor de Destino entre limites, exibidos em formato gráfico. KPIs são usados geralmente por profissionais de negócios para identificar tendências em métricas comerciais críticas.  
  
 Qualquer medida pode servir como a medida Base de um KPI. Para criar um KPI, na grade de medida, clique com o botão direito do mouse na medida e clique em **Criar KPI**. A caixa de diálogo Indicador chave de desempenho aparece e você pode especificar um valor de destino (definido por uma medida ou um valor absoluto) e pode definir limites de status e um tipo gráfico. Para obter mais informações, consulte [KPIs &#40;SSAS de Tabela&#41;](kpis-ssas-tabular.md).  
  
##  <a name="related-tasks"></a><a name="bkmk_rel_tasks"></a> Tarefas relacionadas  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar e gerenciar medidas &#40;SSAS de Tabela&#41;](measures-ssas-tabular.md)|Descreve como criar e gerenciar medidas usando a grade de medida no designer de modelo.|  
  
## <a name="see-also"></a>Consulte Também  
 [KPIs &#40;SSAS de tabela&#41;](kpis-ssas-tabular.md)   
 [Criar e gerenciar KPIs &#40;SSAS de tabela&#41;](create-and-manage-kpis-ssas-tabular.md)   
 [Colunas calculadas &#40;SSAS de Tabela&#41;](ssas-calculated-columns.md)  
  
  
