---
title: Configurar propriedades de relatório para relatórios de Power View | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03afd5bdafe30a8684165fef5febae49f210f042
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940207"
---
# <a name="configure-reporting-properties-for-power-view-reports"></a>Configurar propriedades de relatório para relatórios do Power View
  Nesta lição suplementar, você definirá as propriedades de relatório para o projeto Modelo de Vendas pela Internet do Adventure Works. As propriedades de relatório facilitam para os usuários finais o trabalho de selecionar e exibir dados de modelo no Power View. Você também definirá as propriedades para ocultarem determinadas colunas e tabelas, e criará novos dados para usar em gráficos.  
  
 Depois de concluir esta lição e reimplantar o modelo em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] integrada com o SharePoint e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], você poderá criar uma fonte de dados, especificar as informações de conexão de dados, iniciar o Power View e criar relatórios em relação ao modelo.  
  
 Esta lição não descreve como criar e usar relatórios do Power View. Esta lição pretende fornecer aos autores do modelo tabular uma introdução para essas propriedades e configurações que afetam como os dados de modelo serão exibidos no Power View. Para saber mais sobre como criar relatórios do Power View, consulte [Tutorial: Criar um relatório de exemplo no Power View](https://go.microsoft.com/fwlink/?LinkId=221204).  
  
 Tempo estimado para conclusão desta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Esta lição suplementar faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição suplementar, você deve ter concluído todas as lições anteriores.  
  
 Para concluir esta lição suplementar específica, você deverá ter o seguinte:  
  
-   O Modelo de Vendas pela Internet do Adventure Works (concluído por meio deste tutorial) pronto para ser implantado ou já implantado em uma instância do Analysis Services que está sendo executada no modo Tabular.  
  
-   Um site do SharePoint integrado com o [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] executado em modo de Tabela e o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], configurado para dar suporte a relatórios do Power View.  
  
-   Você deve ter permissões suficientes para criar uma conexão de dados no site do SharePoint que aponta para o Modelo de Vendas pela Internet do Adventure Works.  
  
## <a name="model-properties-that-affect-reporting"></a>Propriedades do modelo que afetam o relatório  
 Ao criar um modelo tabular, há determinadas propriedades que você pode definir em colunas individuais e tabelas para aprimorar a experiência de relatório do usuário final no Power View. Além disso, você pode criar dados de modelo adicionais para dar suporte à visualização de dados e outros recursos específicos para o cliente de relatório. Para o Modelo de Vendas pela Internet do Adventure Works de exemplo, aqui estão algumas das alterações que você fará:  
  
-   **Adicionar novos dados** -adicionar novos dados em uma coluna calculada usando uma fórmula DAX cria informações de data em um formato que é mais fácil de exibir em gráficos.  
  
-   **Ocultar tabelas e colunas que não são úteis para o usuário final** – A propriedade **Hidden** controla se as tabelas e colunas de tabela são exibidas no cliente de relatório. Os itens que estão ocultos ainda fazem parte do modelo e permanecem disponíveis para consultas e cálculos.  
  
-   **Habilitar tabelas com um clique** -por padrão, nenhuma ação ocorrerá se um usuário final clicar em uma tabela na lista de campos. Para alterar este comportamento de modo que um clique na tabela adicione a tabela ao relatório, você definirá o Conjunto de Campos Padrão em cada coluna que você deseja incluir na tabela. Esta propriedade é definida nas colunas da tabela que os usuários finais provavelmente desejarão usar.  
  
-   **Definir o agrupamento quando necessário** – A propriedade **Keep Unique Rows** determina se os valores na coluna devem ser agrupados por valores em um campo diferente, como um campo de identificador. Para colunas que contêm valores duplicados como Nome de Cliente (por exemplo, vários clientes com o nome de Bruno Dias), é importante agrupar (manter linhas exclusivas) no campo **Identificador de Linha** para fornecer aos usuários finais os resultados corretos.  
  
-   **Definir tipos e formatos de dados** – Por padrão, o Power View aplica regras com base no tipo de dados de coluna para determinar se o campo pode ser usado como uma medida. Como cada visualização de dados no Power View também tem regras sobre em que local as medidas e as não medidas podem ser colocadas, é importante definir o tipo de dados no modelo ou substituir o padrão, para obter o comportamento desejado para o usuário final.  
  
-   **Defina a propriedade classificar por coluna** – a propriedade **classificar por coluna** especifica se os valores na coluna devem ser classificados por valores em um campo diferente. Por exemplo, na coluna Calendário do Mês que contém o nome do mês, classifique pela coluna Número do Mês.  
  
## <a name="hide-tables-from-client-tools"></a>Ocultar as tabelas das ferramentas de cliente  
 Como já existe uma coluna calculada Categoria do Produto e Subcategoria do Produto na tabela Produto, não é necessário ter as tabelas Categoria do Produto e Subcategoria do Produto visível para aplicativos cliente.  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>Para ocultar as tabelas Categoria do Produto e Subcategoria do Produto  
  
1.  No designer de modelos, clique com o botão direito do mouse na tabela **Categoria do Produto** (guia) e clique em **Ocultar das Ferramentas de Cliente**.  
  
2.  Clique com o botão direito do mouse na tabela **Subcategoria do Produto** (guia) e clique em **Ocultar das Ferramentas de Cliente**.  
  
## <a name="create-new-data-for-charts"></a>Criar novos dados para gráficos  
 Muitas vezes, pode ser necessário criar novos dados em seu modelo usando fórmulas DAX. Nesta tarefa, você adicionará duas novas colunas calculadas à tabela Data. Estas novas colunas fornecerão campos de data em um formato conveniente para serem usados em gráficos.  
  
#### <a name="to-create-new-data-for-charts"></a>Para criar novos dados para gráficos  
  
1.  Na tabela **Data** , role a tela para a extrema direita e clique em **Adicionar Coluna**.  
  
2.  Adicione duas novas colunas calculadas usando as fórmulas a seguir na barra de fórmulas:  
  
    |Nome da coluna|Fórmula|  
    |-----------------|-------------|  
    |Ano Trimestre|= [Ano civil] & "Q" & [trimestre do calendário]|  
    |Ano Mês|= [Ano civil] & FORMAT([Mês],"#00")|  
  
## <a name="default-field-set"></a>Conjunto de Campos Padrão  
 O Conjunto de Campos Padrão é uma lista predefinida de colunas e medidas para uma tabela que são adicionadas automaticamente a uma tela de relatório do Power View quando a tabela é clicada na lista de campos de relatório. Essencialmente, você pode especificar as colunas padrão, as medidas e a ordenação de campos que os usuários desejarão ver quando esta tabela for visualizada em relatórios do Power View.  Para o modelo de Vendas pela Internet, você definirá um conjunto de campos padrão e ordem para as tabelas Customer, Geography e Product. Incluídas estão somente as colunas mais comuns que os usuários desejarão ver ao analisarem os dados de Vendas pela Internet do Adventure Works usando os relatórios do Power View.  
  
 Para obter informações detalhadas sobre o Conjunto de Campos Padrão, consulte [Configurar o conjunto de campos padrão para relatórios do Power View &#40;SSAS Tabular&#41;](tabular-models/power-view-configure-default-field-set-for-reports.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-default-field-set-for-tables"></a>Para definir o Conjunto de Campos Padrão para tabelas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , em **Propriedades de Relatório**, na propriedade **Conjunto de Campos Padrão** , clique em **Clique para editar** para abrir a caixa de diálogo **Conjunto de Campos Padrão** .  
  
3.  Na caixa de diálogo **Conjunto de Campos Padrão** , na caixa de listagem **Campos na tabela** , pressione Ctrl e selecione os campos a seguir e clique em **Adicionar**.  
  
     **Birth Date**, **Customer Alternate Id**, **First Name**e **Last Name**.  
  
4.  Na janela **Campos padrão, na ordem** , use os botões Mover para Cima e Mover para Baixo para colocar na seguinte ordem:  
  
     **Customer Alternate Id**  
  
     **First Name**  
  
     **Sobrenome**  
  
     **Data de nascimento**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Conjunto de Campos Padrão** da tabela **Customer** .  
  
6.  Realize estas mesmas etapas para a tabela **Geography** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
     **Cidade**, **código de província do estado**, **código da região do estado**.  
  
7.  Por fim, realize estas mesmas etapas para a tabela **Product** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
     **Product Alternate Id**e **Product Name**.  
  
## <a name="table-behavior"></a>Comportamento de tabela  
 Usando as propriedades do Comportamento da Tabela, você pode alterar o comportamento padrão para diferentes tipos de visualização e o comportamento de agrupamento para tabelas usadas nos relatórios do Power View. Isto permite uma melhor colocação padrão de identificação de informações como nomes, imagens ou títulos em layouts de peça, cartão e gráfico.  
  
 Para obter informações detalhadas sobre as propriedades de Comportamento de Tabela, consulte [Configurar propriedades de Comportamento de Tabela de relatórios do Power View &#40;SSAS Tabular&#41;](tabular-models/power-view-configure-table-behavior-properties-for-reports.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-table-behavior-for-tables"></a>Para definir o Comportamento da Tabela para tabelas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , na propriedade **Comportamento da Tabela** , clique em **Clique para editar**, para abrir a caixa de diálogo **Comportamento da Tabela** .  
  
3.  Na caixa de diálogo **Comportamento da Tabela** , na caixa de listagem suspensa **Identificador de Linha** , selecione a coluna **Customer Id** .  
  
4.  Na caixa de listagem **Manter Linhas Exclusivas** , selecione **First Name** e **Last Name**.  
  
     As configurações dessa propriedade especificam que essas colunas fornecem valores que devem ser tratados como exclusivos mesmo se forem duplicados (por exemplo, nome e sobrenome do funcionário, quando dois ou mais funcionários têm o mesmo nome).  
  
5.  Na caixa de listagem suspensa **Rótulo Padrão** , selecione a coluna **Last Name** .  
  
     As configurações dessa propriedade especificam que esta coluna fornece um nome para exibição para representar os dados de linha.  
  
6.  Repita estas etapas para a tabela **Geography** , selecionando a coluna **Geography Id** como o Identificador de Linha e a coluna **City** na caixa de listagem **Manter Linhas Exclusivas** . Você não precisa definir um Rótulo Padrão para esta tabela.  
  
7.  Repita estas etapas para a tabela **Product** , selecionando a coluna **Product Id** como o Identificador de Linha e a coluna **Product Name** na caixa de listagem **Manter Linhas Exclusivas** . Em **Rótulo Padrão**, selecione **Product Alternate Id**.  
  
## <a name="reporting-properties-for-columns"></a>Propriedades de relatório para colunas  
 Há várias propriedades básicas de coluna e propriedades específicas de relatório nas colunas que você pode definir para melhorar a experiência de relatório do modelo. Por exemplo, pode não ser necessário que os usuários vejam todas as colunas em todas as tabelas. Assim como você ocultou as tabelas de categoria de produto e subcategoria de produto anteriormente, usando a Propriedade Hidden de uma coluna, você pode ocultar colunas específicas de uma tabela que, de outra forma, é mostrada. Outras propriedades, como Formato de Dados e Classificar por Coluna, também podem afetar o modo como os dados da coluna podem aparecer nos relatórios. Você definirá algumas dessas propriedades em colunas específicas agora. Outras colunas não exigem nenhuma ação e não são mostradas abaixo.  
  
 Você somente definirá algumas propriedades de coluna diferentes aqui, mas há muitas outras. Para obter mais informações detalhadas sobre as propriedades de relatórios de colunas, consulte [Propriedades de coluna &#40;SSAS Tabular&#41;](tabular-models/properties-ssas-tabular.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-properties-for-columns"></a>Para definir propriedades para colunas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Clique na coluna **Customer Id** para exibir as propriedades de coluna na janela **Propriedades** .  
  
3.  Na janela **Propriedades** , defina a propriedade **Hidden** como True. A coluna **Customer Id** torna-se acinzentada no designer de modelos.  
  
4.  Repita estas etapas, definindo a coluna e as propriedades de relatório a seguir para cada tabela especificada. Deixe todas as outras propriedades em suas configurações padrão.  
  
     **Cliente**  
  
    |Coluna|Propriedade|Valor|  
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |Birth Date|Formato de Dados|Data Abreviada|  
  
     **Data**  
  
    > [!NOTE]  
    >  Como a tabela Date foi selecionada como a tabela de datas do modelo usando a configuração Marcar como Tabela de Data, na Lição 7: Marcar como Tabela de Data, e a coluna Date na tabela Date como a coluna a ser usada como o identificador exclusivo, a propriedade Identificador de Linha para a coluna Date será automaticamente definida como True e não poderá ser alterada. Ao usar as funções de inteligência de tempo em fórmulas DAX, você deverá especificar uma tabela de data. Neste modelo, você criou várias medidas usando funções de inteligência de tempo para calcular dados de vendas para vários períodos como trimestres anterior e atual, e também para usar em KPIs. Para obter mais informações sobre como especificar uma tabela de data, consulte [Especificar Marcar como Tabela de Data para uso com a inteligência de dados temporais &#40;SSAS Tabular&#41;](tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md) nos Manuais Online do SQL Server.  
  
    |Coluna|Propriedade|Valor|  
    |------------|--------------|-----------|  
    |Data|Formato de Dados|Data Abreviada|  
    |Day Number of Week|Hidden|True|  
    |Day Name|Sort By Column|Day Number of Week|  
    |Day Of Week|Hidden|True|  
    |Day of Month|Hidden|True|  
    |Day of Year|Hidden|True|  
    |Month Name|Sort By Column|Mês|  
    |Mês|Hidden|True|  
    |Month Calendar|Hidden|True|  
    |Fiscal Quarter|Hidden|True|  
    |Fiscal Year|Hidden|True|  
    |Fiscal Semester|Hidden|True|  
  
     **Geografia**  
  
    |Coluna|Propriedade|Valor|  
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
  
     **Produto**  
  
    |Coluna|Propriedade|Valor|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Product Alternate Id|Rótulo Padrão|True|  
    |Product Subcategory Id|Hidden|True|  
    |Product Start Date|Formato de Dados|Data Abreviada|  
    |Product End Date|Formato de Dados|Data Abreviada|  
    |Large Photo|Hidden|True|  
  
     **Vendas pela Internet**  
  
    |Coluna|Propriedade|Valor|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Customer Id|Hidden|True|  
    |Promotion Id|Hidden|True|  
    |Currency Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
    |Order Quantity|Tipo de Dados<br /><br /> Formato de Dados<br /><br /> Casas Decimais|Número Decimal<br /><br /> Número Decimal<br /><br /> 0|  
    |Data do Pedido|Tipo de Dados|Data Abreviada|  
    |Due Date|Tipo de Dados|Data Abreviada|  
    |Ship Date|Tipo de Dados|Data Abreviada|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Reimplantar o modelo de tabela de vendas pela Internet da Adventure Works  
 Como você alterou o modelo, deverá reimplantá-lo. Basicamente, você repetirá as tarefas realizadas na [Lição 14: Implantar](lesson-13-deploy.md).  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Para reimplantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Criar** e clique em **Implantar Modelo de Tabela de Vendas pela Internet do Adventure Works**.  
  
     A caixa de diálogo **implantar** é exibida e exibe o status da implantação dos metadados, bem como cada tabela incluída no modelo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora você pode usar o Power View para visualizar dados do modelo. Verifique se as contas do Analysis Services e do Reporting Services no site do SharePoint têm permissões de leitura para a instância do Analysis Services onde você implantou seu modelo.  
  
 Para criar uma fonte de dados de relatório do Reporting Services que aponta para seu modelo, consulte [Tipo de conexão de modelo de tabela (SSRS)](https://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx).  
  
  
