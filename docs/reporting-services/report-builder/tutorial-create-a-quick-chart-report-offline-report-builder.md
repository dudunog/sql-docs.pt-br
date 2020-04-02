---
title: 'Tutorial: Criar um relatório de gráficos rápido offline (Construtor de Relatórios) | Microsoft Docs'
description: Neste tutorial, você cria um gráfico de pizza em um relatório paginado do Reporting Services no Construtor de Relatórios. Em seguida, você adiciona porcentagens e modifica o gráfico de pizza.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41e26cbdeaa794ebae01371207d7ff7847619dc2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290742"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>Tutorial: Criar um relatório de gráficos rápido offline (Construtor de Relatórios)

  Neste tutorial, você usa um Assistente para criar um gráfico de pizza em um relatório paginado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Em seguida, adicione porcentagens e modifique um pouco o gráfico de pizza. 
  
É possível executar este tutorial de duas formas. Os dois métodos têm o mesmo resultado: um gráfico de pizza semelhante ao desta ilustração:  
  
 ![Gráfico de pizza rápido do Construtor de Relatórios](../../reporting-services/report-builder/media/report-builder-quick-pie-chart.png "Gráfico de pizza rápido do Construtor de Relatórios")  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Se você usa dados XML ou uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)], precisa ter acesso ao Construtor de Relatórios. Você pode iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo nativo ou no modo integrado do SharePoint, ou você pode baixar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do Centro de Download da Microsoft. Para obter mais informações, consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md).  
  
##  <a name="two-ways-to-do-this-tutorial"></a><a name="TwoWays"></a> Duas formas de executar este tutorial  
  
-   [Criar o gráfico de pizza com dados XML](#CreatePieChartXML)  
  
-   [Criar o gráfico de pizza com uma consulta Transact-SQL que contém dados](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>Usando dados XML para este tutorial  
 Você pode usar os dados XML que copiar deste tópico e colar no assistente. Não é necessário estar conectado a um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo nativo ou no modo integrado do SharePoint nem ter acesso a uma instância do SQL Server.  
  
 [Criar o gráfico de pizza com dados XML](#CreatePieChartXML)  
  
### <a name="using-a-tsql-query-that-contains-data-for-this-tutorial"></a>Usando uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] contendo dados para este tutorial  
 Você pode copiar uma consulta com dados incluídos neste tópico e colá-la no assistente. Você precisará do nome de uma instância do SQL Server e de credenciais suficientes para ter acesso somente leitura a qualquer banco de dados. A consulta de conjunto de dados no tutorial usa dados literais, mas a consulta deve ser processada por uma instância do SQL Server para retornar os metadados necessários para um conjunto de dados de relatório.  
  
 A vantagem de usar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] é que todos os outros tutoriais do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] usam o mesmo método; portanto, quando você executar os outros tutoriais, já saberá o que fazer.  
  
 A consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] requer outros pré-requisitos. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
 [Criar o gráfico de pizza com uma consulta Transact-SQL que contém dados](#CreatePieQueryData)  
  
##  <a name="creating-the-pie-chart-with-xml-data"></a><a name="CreatePieChartXML"></a> Criando o gráfico de pizza com dados XML  
  
1.  [Inicie o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md) do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , ou do servidor de relatório no modo integrado do SharePoint, ou do seu computador.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
     ![Introdução do Construtor de Relatórios](../../reporting-services/media/rb-getstarted.png "Introdução do Construtor de Relatórios")  
  
     Se a caixa de diálogo **Guia de Introdução** não aparece, clique em **Arquivo** >**Novo**. A maior parte do conteúdo na caixa de diálogo **Novo Relatório ou Conjunto de Dados** é igual àquele encontrado na caixa de diálogo **Introdução** .  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**e em **Criar**.  
  
4.  Na página **Escolha um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolha uma conexão com uma fonte de dados** , clique em **Novo**.  
  
     A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
6.  Você pode atribuir qualquer nome desejado a uma fonte de dados. Na caixa **Nome** , digite **MyPieChart**.  
  
7.  Na caixa **Selecione o tipo de conexão** , clique em **XML**.  
  
8.  Clique na guia **Credenciais** e selecione **Utilizar usuário atual do Windows. A delegação do Kerberos pode ser necessária**. Portanto, clique em **OK**.  
  
9. Na página **Escolha uma conexão com uma fonte de dados** , clique em **MyPieChart**e em **Avançar**.  
  
10. Copie o texto a seguir e cole-o na caixa grande na parte superior da página **Crie uma consulta** .  
  
    ```  
    <Query>  
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>  
    <XmlData>  
    <Root>  
    <S Sales="150">  
      <C FullName="Jae Pak" />  
    </S>  
    <S Sales="350">  
      <C FullName="Jillian  Carson" />  
    </S>  
    <S Sales="250">  
      <C FullName="Linda C Mitchell" />  
    </S>  
    <S Sales="500">  
      <C FullName="Michael Blythe" />  
    </S>  
    <S Sales="450">  
      <C FullName="Ranjit Varkey" />  
    </S>  
    </Root>  
    </XmlData>  
    </Query>  
    ```  
  
11. (Opcional) Clique no botão **Executar** ( **!** ) para ver os dados em que o gráfico se baseará.  
  
     ![Consulta de Design do Construtor de Relatórios](../../reporting-services/report-builder/media/rb-designquery.png "Consulta de Design do Construtor de Relatórios")  
  
12. Clique em **Próximo**.  
  
13. Na página **Escolha um tipo de gráfico** , clique em **Pizza**e em **Avançar**.  
  
14. Na página **Organizar campos de gráfico**, clique duas vezes no campo **Vendas** na caixa **Campos disponíveis**.  
  
     Observe que ela se transforma automaticamente na caixa **Valores** porque é um valor numérico.  
  
     ![Organizar campos do Assistente do Construtor de Relatórios](../../reporting-services/report-builder/media/rb-wizarrangefields.png "Organizar campos do Assistente do Construtor de Relatórios")  
  
15. Arraste o campo **FullName** da caixa **Campos disponíveis** para a caixa **Categorias** (ou clique duas vezes nela para ir para a caixa **Categorias**) e, em seguida, clique em **Avançar**.  
  
     A página Visualização mostra o novo gráfico de pizza com dados representacionais. A legenda diz Nome Completo 1, Nome Completo 2 etc., em vez dos nomes dos vendedores, e o tamanho das fatias da pizza não é exato. Isso é apenas para lhe dar uma ideia da aparência que o relatório terá.  
  
     ![Nova visualização de gráfico do Construtor de Relatórios](../../reporting-services/report-builder/media/rb-newchartpreview.png "Nova visualização de gráfico do Construtor de Relatórios")  
  
16. Clique em **Concluir**.  
  
     Agora, você vê seu novo relatório de gráfico de pizza no Modo de Exibição de Design, ainda com dados representacionais.  
  
     ![Novo gráfico de pizza no Modo de exibição de Design do Construtor de Relatórios](../../reporting-services/report-builder/media/rb-newpiedesign.png "Novo gráfico de pizza no Modo de exibição de Design do Construtor de Relatórios")  
  
17. Para ver seu gráfico de pizza real, clique em **Executar** na guia **Início** da Faixa de Opções.  
  
     ![Nova execução de gráfico do Construtor de Relatórios](../../reporting-services/report-builder/media/rb-newchartrun.png "Nova execução de gráfico do Construtor de Relatórios")  
  
18. Para continuar a modificar o gráfico de pizza, vá para [Depois que você executar o assistente](#AfterWizard) neste artigo.  
  
##  <a name="creating-the-pie-chart-with-a-tsql-query"></a><a name="CreatePieQueryData"></a> Criando o gráfico de pizza com uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
1.  [Inicie o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md) por meio do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , do servidor de relatórios no modo integrado do SharePoint ou em seu computador.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo **Guia de Introdução** não aparece, clique em **Arquivo** >**Novo**. A maior parte do conteúdo na caixa de diálogo **Novo Relatório ou Conjunto de Dados** é igual àquele encontrado na caixa de diálogo **Introdução** .  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**e em **Criar**.  
  
4.  Na página **Escolha um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolha uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou navegue até o servidor de relatório e selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    >  A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
6.  Na página **Crie uma Consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (Opcional) Clique no botão Executar ( **!** ) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Próximo**.  
  
10. Na página **Escolha um tipo de gráfico** , clique em **Pizza**e em **Avançar**.  
  
11. Na página **Organizar campos de gráfico**, clique duas vezes no campo **Vendas** na caixa **Campos disponíveis**.  
  
     Observe que ela se transforma automaticamente na caixa **Valores** , porque esse é um valor numérico.  
  
12. Arraste o campo **FullName** da caixa **Campos disponíveis** para a caixa **Categorias** (ou clique duas vezes nela para ir para a caixa **Categorias**) e, em seguida, clique em **Avançar**.  
  
13. Clique em **Concluir**.  
  
     Você está olhando agora para seu novo relatório de gráfico de pizza na superfície de design. O que você vê é uma representação. A legenda diz Nome Completo 1, Nome Completo 2 etc., em vez dos nomes dos vendedores, e o tamanho das fatias da pizza não é exato. Isso é apenas para lhe dar uma ideia da aparência que o relatório terá.  
  
15. Para ver seu gráfico de pizza real, clique em **Executar** na guia **Início** da Faixa de Opções.  
 
##  <a name="after-you-run-the-wizard"></a><a name="AfterWizard"></a> Depois que você executar o assistente  
 Agora que você tem seu relatório de gráfico de pizza, pode brincar com ele. Na guia **Executar** da Faixa de Opções, clique em **Design**, para que você possa continuar modificando-o.  
  
## <a name="make-the-chart-bigger"></a>Aumentar o gráfico  
 Você optar por aumentar o tamanho do gráfico de pizza. 
 
*  Clique no gráfico, mas não em qualquer elemento do gráfico, para selecioná-lo e arraste o canto inferior direito para redimensioná-lo.  

Observe que a superfície de design fica maior à medida que você arrasta.
  
## <a name="add-a-report-title"></a>Adicionar um título a um relatório  
1. Selecione as palavras **Título do gráfico** na parte superior do gráfico e digite um título, como **Gráfico de Pizza de Vendas**.  
2. Com o título selecionado, no painel Propriedades, altere **Color** para **Black** e **FontSize** para **12pt**.
  
## <a name="add-percentages"></a>Adicionar porcentagens  
 
1.  Clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar Rótulos de Dados**. Os rótulos de dados aparecem dentro de cada fatia do gráfico de pizza.  
  
2.  Clique com o botão direito do mouse nos rótulos e selecione **Propriedades do Rótulo de Série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.  
  
3.  Na caixa **Rotular dados**, digite **#PERCENT{P0}** .  
  
     O **{P0}** fornece o percentual sem casas decimais. Se você digitar apenas **#PERCENT**, os números terão duas casas decimais. **#PERCENT** é uma palavra-chave que executa um cálculo ou uma função para você; há muitas outras.  
     
4. Clique em **Sim** para confirmar que deseja definir **UseValueAsLabel** como **False**.

5. Na guia **Fonte** , selecione **Negrito** e altere **Cor** para **Branco**.

6. Clique em **OK**.     
  
 Para saber mais sobre como personalizar legendas e rótulos de gráfico, veja [Exibir valores de porcentagem em um gráfico de pizza e &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) e [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md).  
  
##  <a name="whats-next"></a><a name="WhatsNext"></a> O que vem a seguir?  
 Agora que você criou seu primeiro relatório no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], está pronto tentar os outros tutoriais e começar a criar relatórios com seus próprios dados. Para executar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], você deve ter permissão para acessar suas fontes de dados, como bancos de dados, com uma *cadeia de conexão* que realmente conecte você à fonte de dados. O administrador do sistema terá essas informações e poderá configurá-las.  
  
 Para trabalhar nos outros tutoriais, você precisa do nome de uma instância do SQL Server e de credenciais suficientes para ter acesso somente leitura a qualquer banco de dados. O administrador do sistema também pode definir isso para você.  
  
 Finalmente, para salvar seus relatórios em um servidor de relatório ou site do SharePoint integrado a um servidor de relatório, você precisa da URL e de permissões. Você pode executar qualquer relatório que criar diretamente de seu computador, mas os relatórios têm mais funcionalidade quando executados no servidor de relatório ou site do SharePoint. Você precisa de permissões para executar seus relatórios ou de outras pessoas no servidor de relatório ou site do SharePoint em que eles foram publicados. Fale com o administrador do sistema para obter acesso.  
  
 Talvez seja útil ler sobre alguns dos conceitos e termos antes de começar. Confira [Conceitos do Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md). Além disso, dedique algum tempo ao planejamento, antes de criar seu primeiro relatório. Esse será um tempo bem gasto. Veja [Planejando um relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md).  

## <a name="next-steps"></a>Próximas etapas

[Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)   
[Construtor de Relatórios no SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
