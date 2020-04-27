---
title: Parâmetros de relatório (Construtor de Relatórios e Designer de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.subreportproperties.parameters.f1
- sql12.rtp.rptdesigner.reportparameters.general.f1
- "10091"
- "10073"
- "10070"
- sql12.rtp.rptdesigner.reportparameters.advanced.f1
ms.assetid: 58b96555-d876-4f61-bff8-db5764b9f5f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9047073a39076fd246b14db26ca1d519fd2e1c6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105073"
---
# <a name="report-parameters-report-builder-and-report-designer"></a>Parâmetros de relatório (Construtor de Relatórios e Designer de Relatórios)
  Este tópico descreve os usos comuns dos parâmetros de relatório SSRS, as propriedades que você pode definir e muito mais sobre os parâmetros. Parâmetros de relatório o habilitam a controlar dados de relatório, conectar relatórios relacionados e variar a apresentação do relatório.  
  
[!INCLUDE[applies](../../includes/applies-md.md)]Modo do SharePoint e modo nativo
  
 Para obter mais informações sobre como adicionar um parâmetro a um relatório, consulte o [Tutorial: adicionando parâmetros a um relatório (SSRS)](https://technet.microsoft.com/library/aa337432\(v=SQL.105\).aspx)  

  
##  <a name="common-uses-for-parameters"></a><a name="bkmk_Common_Uses_for_Parameters"></a> Usos comuns para parâmetros  
 Estas são as formas mais comuns de usar parâmetros.  
  
 **Controlar dados do relatório**  
  
-   Filtrar os dados de relatório na fonte de dados criando consultas de conjunto de dados que contenham variáveis.  
  
-   Filtre os dados de um conjunto de dados compartilhado. Quando você adiciona um conjunto de dados compartilhado a um relatório, não é possível alterar a consulta. No relatório, é possível adicionar um filtro de conjunto de dados que inclua uma referência a um parâmetro de relatório que você criou.  
  
-   Permita que os usuários especifiquem valores para personalizar os dados em um relatório. Por exemplo, forneça dois parâmetros para a data de início e data de término em dados de vendas.  
  
 **Conectar-se a relatórios relacionados**  
  
-   Utilize parâmetros para relacionar relatórios principais a relatórios detalhados, a sub-relatórios e a relatórios vinculados. Ao criar um conjunto de relatórios, geralmente você pode criar cada relatório para responder a determinadas questões. Cada relatório pode fornecer uma exibição diferente ou um nível diferente de detalhes das informações relacionadas. Para fornecer um conjunto de relatórios inter-relacionados, crie parâmetros para os dados relacionados nos relatórios de destino.  
  
     Para obter mais informações, consulte [Relatórios de detalhamento &#40;Construtor de Relatórios e SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md), [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](subreports-report-builder-and-ssrs.md) e [Criar um relatório vinculado](../reports/create-a-linked-report.md).  
  
-   Personalize conjuntos de parâmetros para vários usuários. Crie dois relatórios vinculados com base em um relatório de vendas no servidor de relatório. Um relatório vinculado usa valores de parâmetro predefinidos para vendedores e o outro usa valores de parâmetro predefinidos para gerentes de vendas. Os dois relatórios usam a mesma definição de relatório.  
  
 **Variar apresentação do relatório**  
  
-   Enviar comandos a um servidor de relatório por meio de uma solicitação de URL, para personalizar a renderização de um relatório. Para obter mais informações, consulte [Acesso à URL &#40;SSRS&#41;](../url-access-ssrs.md) e [Passar um parâmetro de relatório em uma URL](../pass-a-report-parameter-within-a-url.md).  
  
-   Permita que os usuários especifiquem valores para ajudar a personalizar a aparência de um relatório. Por exemplo, forneça um parâmetro booliano para indicar se é para expandir ou recolher todos os grupos de linhas aninhados em uma tabela.  
  
-   Permitir que usuários personalizem dados e aparência de relatório incluindo os parâmetros em uma expressão.  
  
     Para obter mais informações, consulte [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md).  
  
##  <a name="parameter-pane"></a><a name="UserInterface"></a>Painel de parâmetros  
 Ao visualizar um relatório, a barra de ferramentas do visualizador de relatórios exibe cada parâmetro de forma que um usuário possa especificar valores de maneira interativa. A ilustração a seguir mostra a área de parâmetro para um relatório que @StartDatetem @EndDateparâmetros @Subcategory,, @ShowAllRowse.  
  
 ![rs_ParameterStory](../media/rs-parameterstory.gif "rs_ParameterStory")  
  
1.  **Painel de parâmetros** A barra de ferramentas do visualizador de relatórios exibe um aviso e valor padrão para cada parâmetro. O layout do parâmetro na barra de ferramentas é formatado automaticamente. A ordem é determinada pela ordem dos parâmetros exibidos no painel de Dados do Relatório.  
  
2.  **@StartDatee @EndDate parâmetros** o parâmetro @StartDate é tipo `DateTime`de dados. O aviso Data de Início é exibido ao lado da caixa de texto. Para modificar a data, digite uma nova data na caixa de texto ou use o controle de calendário.  
  
     O parâmetro @EndDate é exibido ao @StartDatelado de.  
  
3.  ** @Subcategory parâmetro** do O parâmetro @Subcategory é o tipo `Text`de dados. Como @Subcategory o tem uma lista de valores disponíveis, os valores válidos aparecem em uma lista suspensa. Você deve escolher os valores nessa lista. Como @Subcategory é de valores de multivalor, é exibida uma opção **selecionar tudo** que permite limpar todos e selecionar todos os valores na lista.  
  
4.  ** @ShowAllRows parâmetro** do O parâmetro @ShowAllRows é o tipo `Boolean`de dados. Use os botões de opção para especificar `True` ou `False`.  
  
5.  **Identificador Mostrar ou Ocultar Área de Parâmetros** Na barra de ferramentas do visualizador de relatórios, clique nessa seta para mostrar ou ocultar o painel de parâmetros.  
  
6.  **Botão Parâmetros** Na visualização do Construtor de Relatórios, na Faixa de Opções, clique no botão **Parâmetros** para mostrar ou ocultar o painel de parâmetros.  
  
7.  **Botão Exibir Relatório** Na barra de ferramentas do visualizador de relatórios, clique em **Exibir Relatório** para executar o relatório depois de inserir valores de parâmetro. Se todos os parâmetros tiverem valores padrão, o relatório será executado automaticamente na primeira exibição.  
  
##  <a name="creating-parameters"></a><a name="bkmk_Create_Parameters"></a> Criar parâmetros  
 Você pode criar parâmetros de relatório das seguintes maneiras:  
  
-   Adicionar uma consulta de conjunto de dados que contenha variáveis ou um procedimento armazenado de banco de dados que contenha parâmetros de entrada. Um parâmetro de conjunto de dados é criado para cada variável ou parâmetro de entrada e um parâmetro de relatório é criado para cada parâmetro de conjunto de dados.  
  
     A seguinte imagem do Construtor de Relatórios mostra uma consulta de conjunto de dados com uma variável (1), o parâmetro de conjunto de dados (2) correspondente e o parâmetro de relatório (3).  
  
     ![Caixa de diálogo Propriedades do Conjunto de Dados e Painel de Relatórios](../media/datasetquery-parameters.png "Caixa de diálogo Propriedades do Conjunto de Dados e Painel de Relatórios")  
  
    > **ANOTAÇÕES!** Nem todas as fontes de dados oferecem suporte a parâmetros.  
  
     O conjunto de dados pode ser inserido ou compartilhado. Ao adicionar um conjunto de dados compartilhado a um relatório, os parâmetros de conjunto de dados marcados como internos não poderão ser substituídos no relatório. Você poderá substituir os parâmetros de conjunto de dados que não estiverem marcados como internos.  
  
     Para obter mais informações, consulte [Consulta de conjuntos de dados](#bkmk_Dataset_Parameters) neste tópico.  
  
-   Crie um parâmetro manualmente a partir do painel de Dados do Relatório.  
  
     É possível configurar os parâmetros de relatório de forma que um usuário possa inserir valores interativamente para ajudar a personalizar o conteúdo ou a aparência de um relatório. Você também pode configurar parâmetros de relatório de forma que um usuário não possa alterar os valores pré-configurados.  
  

  > **ANOTAÇÕES!** Como os parâmetros são gerenciados independentemente no servidor, a republicação de um relatório principal com novas configurações de parâmetros não substituirá as configurações de parâmetros existentes no relatório.  
  
-   Adicione uma parte de relatório que contenha referências a um parâmetro ou a um conjunto de dados compartilhado que contém variáveis.  
  
     As partes de relatório são armazenadas no servidor de relatório e disponibilizadas para uso em relatórios de outras pessoas. As partes de relatório que são parâmetros não podem ser gerenciados de um servidor de relatório. Você pode procurar parâmetros na Galeria de Partes de Relatório e, depois de adicioná-los, configurá-los em seu relatório. Para obter mais informações, consulte [partes de relatório &#40;Construtor de relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
     
   > **ANOTAÇÕES!** Parâmetros podem ser publicados como uma parte de relatório separada para regiões de dados que têm conjuntos de dados dependentes com parâmetros. Embora parâmetros sejam listados como parte de um relatório, você não pode acrescentar um parâmetro de parte de relatório diretamente a um relatório. Em vez disso, adicione a parte de relatório, e quaisquer parâmetros de relatório necessários serão gerados automaticamente de consultas de conjunto de dados contidas ou referenciadas pela parte de relatório. Para obter mais informações sobre partes de relatório, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md) e [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](report-parts-in-report-designer-ssrs.md).  
  
### <a name="parameter-values"></a>Valores dos parâmetros  
 As seguintes opções servem para seleção de valores de parâmetro em um relatório.  
  
-   Selecione um valor de parâmetro único da lista suspensa.  
  
-   Selecione vários valores de parâmetro da lista suspensa.  
  
-   Selecione um valor da lista suspensa para um parâmetro, o qual determina os valores que estão disponíveis na lista suspensa para outro parâmetro. Esses são parâmetros em cascata. Parâmetros em cascata permitem que você filtre milhares de valores de parâmetro sucessivamente para obter um número gerenciável.  
  
     Para obter mais informações, consulte [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
-   Execute o relatório sem precisar primeiro selecionar um valor de parâmetro porque um valor padrão foi criado para o parâmetro.  
  
##  <a name="report-parameter-properties"></a><a name="bkmk_Report_Parameters"></a>Propriedades do parâmetro de relatório  
 É possível alterar as propriedades de parâmetros de relatório usando a caixa de diálogo de Propriedades do Relatório. A tabela a seguir resume as propriedades que você pode definir para cada parâmetro:  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|Nome|Digite um nome com diferenciação de maiúsculas e minúsculas para o parâmetro. O nome deve começar com uma letra e pode conter letras, números e sublinhado (_). O nome não pode conter espaços. Para parâmetros gerados automaticamente, o nome corresponde ao parâmetro na consulta de conjunto de dados. Por padrão, parâmetros criados manualmente são semelhantes a ReportParameter1.|  
|Prompt|O texto que aparece ao lado do parâmetro na barra de ferramentas do visualizador de relatórios.|  
|Tipo de dados|Quando os valores disponíveis são definidos para um parâmetro, o usuário escolhe valores de uma lista suspensa, mesmo quando o tipo de dados é `DateTime`. Um parâmetro de relatório deve ser de um destes tipos de dados:<br /><br /> `Boolean`. O usuário seleciona Verdadeiro ou Falso usando um botão de opção.<br /><br /> `DateTime`. O usuário seleciona uma data usando um controle de calendário.<br /><br /> **Inteiro**. O usuário digita valores em uma caixa de texto.<br /><br /> **Float**. O usuário digita valores em uma caixa de texto.<br /><br /> `Text`. O usuário digita valores em uma caixa de texto.<br /><br /> Para obter mais informações sobre os tipos de dados de relatório, consulte [RDL Data Types](../reports/report-definition-language-ssrs.md#bkmk_RDL_Data_Types).|  
|Permitir valor em branco|Selecione esta opção se o valor do parâmetro puder ser uma cadeia de caracteres vazia ou ficar em branco.<br /><br /> Se você especificar valores válidos para um parâmetro e desejar que um valor em branco seja um dos valores válidos, deverá incluí-lo como um dos valores que especificar. A seleção desta opção não inclui automaticamente um espaço em branco para valores disponíveis.|  
|Permitir valor nulo|Selecione esta opção se o valor do parâmetro puder ser nulo.<br /><br /> Se você especificar valores válidos para um parâmetro e desejar que um valor nulo seja um dos valores válidos, deverá incluir nulo como um dos valores que especificar. A seleção desta opção não inclui um valor nulo automaticamente nos valores disponíveis.|  
|Permitir diversos valores|Forneça valores disponíveis para criar uma lista suspensa na qual seus usuários possam fazer seleções. Essa é uma boa maneira de assegurar que somente valores válidos sejam enviados na consulta de conjunto de dados.<br /><br /> Selecione esta opção se o valor do parâmetro puder ter diversos valores exibidos em uma lista suspensa. Valores nulos são permitidos. Quando essa opção é selecionada, as caixas marcadas são adicionadas à lista de valores disponíveis em uma lista suspensa de parâmetros. A parte superior da lista inclui uma caixa de seleção para **Selecionar Tudo**. Os usuários podem marcar os valores desejados.<br /><br /> Se os dados que fornecem valores forem alterados rapidamente, a lista que o usuário verá talvez não seja a mais atual.|  
|Visible|Selecione esta opção para exibir o parâmetro de relatório na parte superior do relatório quando ele for executado. Esta opção permite que os usuários selecionem valores de parâmetro em tempo de execução.|  
|Hidden|Selecione essa opção para ocultar o parâmetro no relatório publicado. Os valores de parâmetro de relatório ainda podem ser definidos em uma URL de relatório, em uma definição de assinatura ou no servidor de relatório.|  
|Interna|Selecione essa opção para ocultar o parâmetro de relatório. No relatório publicado, o parâmetro de relatório só pode ser exibido na definição do relatório.|  
|Valores disponíveis|Se você especificou valores disponíveis para um parâmetro, os valores válidos sempre aparecerão como uma lista suspensa. Por exemplo, se você fornecer valores disponíveis para um parâmetro `DateTime`, uma lista suspensa para datas aparecerá no painel de parâmetro em vez de um controle de calendário. Para assegurar que uma lista de valores seja consistente em um relatório e sub-relatórios, você poderá definir uma opção na fonte de dados para usar uma única transação para todas as consultas nos conjuntos de dados que forem associados a uma fonte de dados.<br /><br /> Observação de ** \* segurança \* \* ** Em qualquer relatório que inclua um parâmetro de tipo `Text`de dados, certifique-se de usar uma lista de valores disponíveis (também conhecida como uma lista de valores válidos) e certifique-se de que qualquer usuário que esteja executando o relatório tenha apenas as permissões necessárias para exibir os dados no relatório. Para obter mais informações, consulte [Segurança &#40;Construtor de Relatórios&#41;](../report-builder/security-report-builder.md).|  
|Valores padrão|Defina os valores padrão usando uma consulta ou uma lista estática.<br /><br /> Quando cada parâmetro tem um valor padrão válido, o relatório é executado automaticamente na primeira exibição.|  
|Avançado|Defina o atributo de definição de relatório `UsedInQuery`, um valor que indica se o parâmetro em questão afeta direta ou indiretamente os dados de um relatório.<br /><br /> **Determinar automaticamente quando atualizar**<br /> Escolha esta opção para que o processador de relatório determine uma configuração para este valor. O valor será `True` se o processador de relatório detectar uma consulta de conjunto de dados com uma referência direta ou indireta a este parâmetro, ou se o relatório tiver sub-relatórios.<br /><br /> **Atualizar sempre**<br /> Escolha esta opção quando o parâmetro de relatório for usado direta ou indiretamente em uma consulta de conjunto de dados ou em uma expressão de parâmetro. Esta opção define `UsedInQuery` como True.<br /><br /> **Nunca atualizar**<br /> Escolha esta opção quando o parâmetro de relatório não for usado direta ou indiretamente em uma consulta de conjunto de dados ou em uma expressão de parâmetro. Esta opção define `UsedInQuery` como False.<br /><br /> ** \* Cuidado \* \* ** Use **nunca atualizar** com cuidado. No servidor de relatório, `UsedInQuery` é usado para ajudar a controlar as opções de cache para os dados de relatórios e para relatórios renderizados, além de opções de parâmetro para relatórios de instantâneo. Se você definir incorretamente a opção **Nunca Atualizar** , é possível que os dados de relatórios ou os relatórios incorretos sejam armazenados em cache, ou que um relatório de instantâneo apresente dados inconsistentes. Para obter mais informações, consulte [Linguagem RDL &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md).|  
  
##  <a name="dataset-query"></a><a name="bkmk_Dataset_Parameters"></a>Consulta de conjunto de pesquisa  
 Para filtrar dados na consulta de conjunto de dados, você pode incluir uma cláusula de restrição que limite os dados recuperados especificando valores a serem incluídos ou excluídos do conjunto de resultados.  
  
 Use o designer de consulta para a fonte de dados para criar uma consulta parametrizada.  
  
-   Em consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] , diferentes fontes de dados dão suporte a diferentes sintaxes para parâmetros. O suporte abrange parâmetros que são identificados na consulta por posição ou por nome. Para obter mais informações, consulte os tópicos para tipos específicos de fontes de dados externas em [Adicionar dados a um relatório &#40;Construtor de relatórios e SSRS&#41;](../report-data/report-datasets-ssrs.md). No designer de consulta relacional, você deve selecionar a opção de parâmetro para um filtro para poder criar uma consulta parametrizada. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Relacionais &#40;Construtor de Relatórios&#41;](../report-data/relational-query-designer-user-interface-report-builder.md).  
  
-   Para consultas baseadas em uma fonte de dados multidimensional como o Microsoft SQL Server Analysis Services, SAP NetWeaver BI ou Hyperion Essbase, você poderá especificar se um parâmetro será criado com base em um filtro que você definir no criador de consultas. Para obter mais informações, consulte o tópico sobre o designer de consultas em [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md) que corresponda à extensão de dados.  
  
##  <a name="parameter-management-for-a-published-report"></a><a name="bkmk_Manage_Parameters"></a> Gerenciamento de parâmetros para um relatório publicado  
 Quando você cria um relatório, os parâmetros de relatório são salvos na definição de relatório. Quando você publica um relatório, os parâmetros de relatório são salvos e gerenciados separadamente da definição de relatório.  
  
 Para um relatório publicado, você pode usar o seguinte:  
  
-   **Propriedades de parâmetros de relatório.** Altere os valores de parâmetros de relatório diretamente no servidor de relatório, de modo independente da definição de relatório.  
  
-   **Relatórios armazenados em cache.** Para criar um plano de cache para um relatório, cada parâmetro deve ter um valor padrão. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md).  
  
-   **Conjuntos de dados compartilhados armazenados em cache.** Para criar um plano de cache para um conjunto de dados compartilhado, cada parâmetro deve ter um valor padrão. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md).  
  
-   **Relatórios vinculados.** Você pode criar relatórios vinculados com valores de parâmetro predefinidos para filtrar dados para públicos distintos. Para obter mais informações, consulte [Criar um relatório vinculado](../reports/create-a-linked-report.md).  
  
-   **Inscrições de relatório.** Você pode especificar valores de parâmetro para filtrar dados e entregar relatórios por meio de assinaturas. Para obter mais informações, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
-   **Acesso à URL.** Você pode especificar valores de parâmetro em uma URL para um relatório. Também é possível executar relatórios e especificar valores de parâmetros usando o acesso à URL. Para obter mais informações, consulte [Acesso à URL &#40;SSRS&#41;](../url-access-ssrs.md).  
  
 As propriedades de parâmetros para um relatório publicado são geralmente preservadas se você publicar novamente a definição do relatório. Se a definição do relatório for publicada novamente como o mesmo relatório, e os nomes e tipos de dados dos parâmetros continuarem os mesmos, as configurações de propriedades serão retidas. Se você adicionar ou excluir parâmetros da definição do relatório, ou alterar o tipo de dados ou o nome de um parâmetro existente, poderá ser necessário alterar as propriedades dos parâmetros no relatório publicado.  
  
 Nem todos os parâmetros podem ser modificados em todos os casos. Se um parâmetro de relatório obtiver um valor padrão de uma consulta de conjunto de dados, esse valor não poderá ser modificado para um relatório publicado e não poderá ser modificado no servidor de relatório. O valor usado em tempo de execução é determinado quando a consulta é executada ou, no caso de parâmetros baseados em expressão, quando a expressão é avaliada.  
  
 As opções de execução de relatório podem afetar o tipo de processamento dos parâmetros. Um relatório executado como um instantâneo não pode usar parâmetros derivados de uma consulta, a menos que a consulta inclua valores padrão para os parâmetros.  
  
##  <a name="parameters-for-a-subscription"></a><a name="bkmk_Parameters_Subscription"></a> Parâmetros para uma assinatura  
 Você pode definir uma assinatura para um relatório sob demanda ou para um instantâneo e especificar valores de parâmetro a serem usados durante o processamento da assinatura.  
  
-   **Relatório sob demanda.**  Para um relatório sob demanda, você pode especificar um valor de parâmetro diferente do valor publicado para cada parâmetro listado para o relatório. Por exemplo, suponha que você tenha um relatório Serviço de Chamada que usa um parâmetro *Período de Tempo* para retornar solicitações de atendimento ao cliente para o dia, semana ou mês atual. Se o valor de parâmetro padrão do relatório for definido como **hoje**, sua assinatura poderá usar um valor de parâmetro diferente (como **semana** ou **mês**) para produzir um relatório com estatísticas semanais ou mensais.  
  
-   **Instantânea.**  Para um instantâneo, sua assinatura deve usar os valores de parâmetro definidos para o instantâneo. Sua assinatura não pode substituir um valor de parâmetro que está definido para um instantâneo. Por exemplo, suponha que você esteja assinando um relatório de vendas regional ocidental executado como um instantâneo de relatório e que o instantâneo especifique **Ocidental** como um valor de parâmetro regional. Nesse caso, se você criar uma assinatura para esse relatório, deverá usar o valor de parâmetro **Ocidental** em sua assinatura. Para fornecer uma indicação visual de que o parâmetro é ignorado, os campos de parâmetro da página da assinatura são definidos como campos somente leitura.  
  
     As opções de execução de relatório podem afetar o tipo de processamento dos parâmetros. Os relatórios parametrizados executados como instantâneos de relatório usam os valores de parâmetro definidos para o instantâneo de relatório. Os valores de parâmetro estão definidos na página de propriedades de parâmetro do relatório. Um relatório executado como um instantâneo não pode usar parâmetros derivados de uma consulta, a menos que a consulta inclua valores padrão para os parâmetros.  
  
     Se um valor de parâmetro for alterado no instantâneo de relatório após a definição da assinatura, o servidor de relatório desativará a assinatura. A desativação da assinatura indica que o relatório foi modificado. Abra a assinatura e salve-a para ativá-la.  
  
> [!NOTE]  
>  As assinaturas controladas por dados podem usar valores de parâmetro obtidos de uma fonte de dados de assinante. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Para obter mais informações, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
##  <a name="parameters-and-securing-data"></a><a name="bkmk_Parameters_Security"></a> Parâmetros e proteção de dados  
 Tenha cuidado ao distribuir relatórios parametrizados que contêm informações confidenciais. Um usuário pode substituir facilmente um parâmetro de relatório por um valor diferente, resultando na divulgação indevida de informações.  
  
 Uma alternativa segura para usar parâmetros para dados de funcionários ou pessoais é selecionar os dados com base nas expressões que incluem o campo **UserID** da coleção Usuários. A coleção Usuários fornece um meio de obter a identidade do usuário que executa o relatório e de usar essa identidade para recuperar dados específicos do usuário.  
  
> [!IMPORTANT]  
>  Em qualquer relatório que contenha um parâmetro do tipo `String`, use uma lista de valores disponíveis (também conhecida como uma lista de valores válidos) e verifique se todos os usuários que executam o relatório têm as permissões necessárias para exibir os dados do relatório apenas. Quando você define um parâmetro do tipo `String`, é exibida para o usuário uma caixa de texto que pode ter qualquer valor. Uma lista de valores disponíveis limita os valores que podem ser inseridos. Se o parâmetro do relatório estiver associado a um parâmetro de conjunto de dados e uma lista de valores disponíveis não for usada, um usuário do relatório poderá digitar a sintaxe SQL na caixa de texto, abrindo potencialmente o relatório e o servidor a um ataque de injeção de SQL. Se o usuário tiver permissões suficientes para executar a nova instrução SQL, resultados indesejados podem ser produzidos no servidor.  
>   
>  Se um parâmetro de relatório não estiver associado a um parâmetro de conjunto de dados e os valores de parâmetro forem incluídos no relatório, um usuário do relatório poderá digitar a sintaxe de expressão ou uma URL no valor de parâmetro e renderizar o relatório em Excel ou HTML. Se outro usuário exibir o relatório e clicar no conteúdo do parâmetro renderizado, o usuário poderá executar acidentalmente o script ou link mal-intencionado.  
>   
>  Para reduzir o risco de execução acidental de scripts mal-intencionados, só abra relatórios renderizados de fontes confiáveis. Para obter mais informações sobre como proteger relatórios, consulte [Protegendo Relatórios e Recursos](../security/secure-reports-and-resources.md).  
  
##  <a name="how-to-topics"></a><a name="bkmk_How_To_Topics"></a>Tópicos de instruções  
 Esta seção lista procedimentos que mostram, passo a passo, como trabalhar com parâmetros e filtros.  
  
-   [Adicionar, alterar ou excluir um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
-   [Adicionar, alterar ou excluir valores disponíveis para um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md)  
  
-   [Adicionar, alterar ou excluir valores padrão para um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)  
  
-   [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
-   [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)  
  
-   [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
-   [Adicionar um sub-relatório e parâmetros &#40;Construtor de Relatórios e SSRS&#41;](add-a-subreport-and-parameters-report-builder-and-ssrs.md)  
  
-   [Relatório do SSRS para procedimento armazenado com parâmetros](https://www.c-sharpcorner.com/UploadFile/7d3362/ssrs-report-for-parameterize-stored-procedure/)  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos ouvindo  
 Quais são as informações que você está procurando? Você as localizou? Estamos ouvindo seus comentários para melhorar o conteúdo. Envie seus comentários para[sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Report%20Parameters%20page)  
  
##  <a name="related-content"></a><a name="bkmk_Related_Topics"></a> Conteúdo relacionado  
 [Configurando parâmetros de relatório SSRS (teste)](https://www.trenovision.com/quiz/sql-server-reporting-services-ssrs-quiz/)  
  
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
 [Estourando os mistérios de InvalidReportParameterException no serviço de relatório](https://go.microsoft.com/fwlink/p/?LinkId=393118)  
  
 [Exemplos de relatório (Construtor de Relatórios e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
 [Segurança &#40;Construtor de Relatórios&#41;](../report-builder/security-report-builder.md)  
  
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
 [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
