---
title: Localizar, exibir e gerenciar relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
description: No Construtor de Relatórios e no Designer de Relatórios, você pode procurar para localizar relatórios paginados, fontes de dados compartilhadas, modelos e outros itens de relatório relacionados.
ms.date: 12/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 5599300d-6bcd-4704-aba5-fa98e01c78a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 74c4591122fa45d4e050718e78296ed672a4c210
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258100"
---
# <a name="finding-viewing-and-managing-reports-report-builder-and-ssrs-"></a>Localizando, exibindo e gerenciando relatórios (Construtor de Relatórios e SSRS)
  No Construtor de Relatórios, você pode procurar pastas em um servidor de relatório ou site do SharePoint para encontrar relatórios paginados, fontes de dados compartilhadas, modelos e outros itens de relatório relacionados e navegar no computador para localizar relatórios locais. Para facilitar a localização de relatórios, o Construtor de Relatórios mantém uma lista de servidores e sites usados recentemente e fornece acesso direto às pastas Área de Trabalho, Meus Documentos e Meu Computador no sistema de arquivos do computador.  
  
 No Designer de Relatórios, você pode procurar também seu computador para localizar relatórios paginados locais. Depois de implantar relatórios em um servidor de relatório ou site do SharePoint, você pode procurar o servidor de relatório usando o portal da Web, ou pode pesquisar o site do SharePoint para localizar relatórios. Relatórios e itens relacionados permanecem disponíveis localmente após serem implantados.  
  
> [!NOTE]  
> Você pode usar o Construtor de Relatórios no modo local ou conectado a um servidor de relatório. Certas limitações se aplicam quando você não tem uma conexão ativa com um servidor de relatório.  
  
 Para localizar um relatório em um servidor de relatório ou site do SharePoint a partir do Construtor de Relatórios, forneça a URL ao servidor de relatório ou site do SharePoint. Quando você instala o Construtor de Relatórios pela primeira vez, pode especificar a URL a ser usada. Esse é o servidor ou site ao qual o Construtor de Relatórios se conecta por padrão quando você salva ou abre relatórios.  
  
 Os relatórios podem ser exibidos no Construtor de Relatórios e no Designer de Relatórios quando você cria ou atualiza relatórios, e podem ser exibidos e gerenciados em um servidor de relatório com o uso do portal da Web ou em um site do SharePoint integrado ao Reporting Services, usando as ferramentas e os recursos internos do SharePoint após a publicação dos relatórios. Para obter mais informações, consulte [Visualizando relatórios no Construtor de Relatórios](../../reporting-services/report-builder/previewing-reports-in-report-builder.md) e [Visualizando relatórios](../../reporting-services/reports/previewing-reports.md).  
  
 Quando você exibe relatórios no Construtor de Relatórios e no Designer de Relatórios, ou no portal da Web ou em um site do SharePoint, os dados são atualizados e os relatórios exibem os dados atuais da fonte de dados que o relatório usa. Para exibir um relatório sem atualizar seus dados, use o histórico de relatório e os dados calculados com relatórios publicados. Não é possível usar esses recursos durante a visualização de relatórios no Construtor de Relatórios e no Designer de Relatórios.  
  
> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="finding-and-viewing-reports-in-report-builder"></a><a name="FindingAndViewingReportsRB30"></a> Localizando e exibindo relatórios no Construtor de Relatórios  
 Para localizar um relatório com o qual você deseja trabalhar ou para selecionar uma fonte de dados compartilhados, uma imagem ou um sub-relatório a ser usado em um relatório, procure no computador, nas pastas em um servidor de relatório ou em um site do SharePoint integrado ao Reporting Services.  
  
 Para localizar relatórios em um servidor de relatório, você deve especificar uma URL para o servidor de relatório e ter permissões apropriadas nas pastas que lhe permitem ler e salvar itens de relatório. Peça ao administrador do sistema o servidor de relatório para a URL e as permissões apropriadas.  
  
 Depois que encontrar e abrir o relatório no Construtor de Relatórios, você poderá visualizá-lo e fazer alterações. Ao visualizar o relatório, você vê os dados atuais. Para obter mais informações, consulte [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
 O Construtor de Relatórios pode ajudá-lo com as seguintes tarefas:  
  
-   **Localizando relatórios** Quando você procura um relatório, pode usar o estilo familiar da caixa de diálogo **Abrir Arquivo** do Microsoft Office, personalizada para o Construtor de Relatórios. Você pode procurar as pastas em um servidor de relatório ou em um sistema de arquivos, inclusive Meus Relatórios, Sites e Servidores, Área de Trabalho, Meus Documentos, Meu Computador. Sites e Servidores fornece uma lista de servidores usados recentemente.  
  
-   **Localizando fontes de dados compartilhadas** Quando você procura uma fonte de dados compartilhada, pode escolher em uma lista de itens usados recentemente ou navegar até outra pasta no mesmo servidor de relatório do relatório.  
  
-   **Exibindo relatórios** Você visualiza um relatório no Construtor de Relatórios ao criar ou atualizar relatórios. Quando o Construtor de Relatórios está conectado a um servidor de relatório, esse servidor carrega e processa o relatório; caso contrário, os relatórios são processados localmente. O visualizador de relatório no Construtor de Relatórios exibe o relatório renderizado.  
  
 
##  <a name="viewing-and-managing-reports-on-a-report-server"></a><a name="ViewingAndManagingReportServer"></a> Exibindo e gerenciando relatórios em um servidor de relatório  
 É possível usar o portal da Web para exibir e gerenciar relatórios no servidor de relatório. Procure as pastas no servidor para localizar relatórios, executar relatórios para exibi-los em um navegador e executar tarefas de gerenciamento.  
  
 O portal da Web pode ajudar com as seguintes tarefas de gerenciamento:  
  
-   Exiba e atualize as propriedades de relatórios, as fontes de dados compartilhados e outros itens de relatório.  
  
-   Carregue relatórios e crie novas fontes de dados compartilhados para relatórios.  
  
-   Crie cronogramas para executar relatórios em horários e intervalos especificados.  
  
-   Crie, altere ou exclua assinaturas para relatórios.  
  
-   Crie o histórico de relatório e especifique o número de instantâneos de relatórios a serem mantidos no histórico de relatórios.  
  
-   Crie novas pastas no servidor para organizar os relatórios da maneira desejada.  
  
 Algumas dessas tarefas talvez sejam executadas para você pelo administrador do servidor de relatório. Para saber mais sobre as tarefas executadas em um servidor de relatório, consulte [Servidor de Relatório do Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
Em geral, o portal da Web contém pastas, relatórios e fontes de dados, bem como a pasta Meus Relatórios. A pasta Meus Relatórios é um workspace pessoal que pode ser usado para armazenar e trabalhar com seus relatórios e para exibi-los. Outras pastas do servidor de relatórios são públicas e geralmente exigem que os usuários tenham permissões avançadas para adicionar ou modificar o conteúdo de pasta. Você pode criar subpastas em Meus Relatórios para organizar ainda mais seus relatórios.  
  
 O portal da Web exibe relatórios no Visualizador de HTML do Reporting Services. O Visualizador de HTML fornece uma estrutura para a exibição de relatórios em HTML e inclui uma barra de ferramentas de relatório, uma seção de parâmetro, uma seção de credenciais e um mapa do documento. A barra de ferramentas de relatório fornece as funcionalidades de navegação de página, zoom, atualização, pesquisa, exportação, impressão e feed de dados. A barra de ferramentas do relatório também é exibida em uma janela do navegador na parte superior de um relatório quando você acessa relatórios por uma URL. A funcionalidade de impressão é opcional e deve ser ativada pelo administrador. Quando disponível, um ícone Impressora é exibido na barra de ferramentas de relatório. As ilustrações a seguir mostram uma aproximação da barra de ferramentas de relatórios no portal da Web.  
  
 ![Barra de ferramentas de relatório no portal da Web](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/report-toolbar-in-the-web-portal.png)  
  
Após a execução de um relatório, você pode exportá-lo para outro formato, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ou PDF. Também é possível exportar o relatório usando uma extensão de renderização de dados, como CSV, e depois usar o arquivo de dados CSV como entrada para outro aplicativo. Para saber mais sobre os relatórios de exportação, confira [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).
  
 A maneira mais fácil de selecionar e executar um relatório é abrir o portal da Web e procurar ou navegar até o relatório a ser exibido.  
  
 Depois que executar um relatório, você poderá atualizá-lo para visualizar novos dados.  
  
### <a name="refreshing-reports"></a>Atualizando relatórios  
 Com frequência, os dados de relatório são alterados e talvez você queira atualizar o relatório para exibir os dados mais novos. Você pode atualizar um relatório de três modos diferentes.  
  
|Opção|Result|  
|------------|------------|  
|Botão**Atualizar** na janela do navegador|Exibe o relatório armazenado no cache de sessão. Um cache de sessão é criado quando um usuário abre um relatório. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa sessões do navegador para manter uma experiência de exibição consistente enquanto um relatório é aberto.|  
|![Botão Atualizar do navegador na barra de ferramentas de relatório](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/browser-refresh-button-on-report-toolbar.png)|Quando você clica no botão **Atualizar** na barra de ferramentas do relatório, o servidor de relatório executa novamente a consulta e atualiza os dados de relatório caso o relatório execute sob demanda. Se o relatório for armazenado em cache ou for um instantâneo, **Atualizar** será exibido no relatório armazenado no banco de dados do servidor de relatório.|  
|Combinação de teclado CTRL+F5|Produz o mesmo resultado que clicar no botão **Atualizar** na barra de ferramentas do relatório.|  
  
  
##  <a name="viewing-and-managing-report-server-items-from-a-sharepoint-site"></a><a name="ViewingAndManagingSharePointSite"></a> Exibindo e gerenciando itens do servidor de relatórios de um site do SharePoint  
 Quando o administrador de sistema configurar um servidor de relatório para execução em modo integrado do SharePoint, será possível exibir e gerenciar relatórios e demais itens do servidor de relatório a partir do site do SharePoint.  
  
 O site do SharePoint inclui páginas para definir as propriedades da fonte de dados, histórico do relatório, opções de processamento do relatório, agendas, assinaturas, parâmetros de relatórios e para criar agendas compartilhadas. É possível gerenciar os itens do servidor de relatórios em um site do SharePoint do mesmo modo que você cria e gerencia os mesmos a partir de outras ferramentas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para acessar as páginas do aplicativo, selecione ações específicas para itens a partir de um menu suspenso em um relatório ou outro item de servidor de relatórios que você adicionou anteriormente a uma biblioteca do SharePoint. Dependendo do item e suas permissões, você poderá também criar relatórios no Construtor de Relatórios, gerar modelos e definir a segurança de item de modelo.  
  
 Para obter mais informações sobre a tecnologia do SharePoint e do Reporting Services, confira [Configuração e administração de um servidor de relatório &#40;modo do SharePoint do Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).
  
### <a name="finding-report-server-items-on-a-sharepoint-site"></a>Localizando itens de servidor de relatório em um site do SharePoint  
 Antes de poder definir as propriedades, primeiro você deve localizar o item. Os itens do servidor de relatório são sempre armazenados em bibliotecas ou em uma pasta de uma biblioteca.  
  
 Ao acessar o site do SharePoint, você verá a página Procurar e a guia de Ferramentas de Biblioteca. A página Procurar relaciona as bibliotecas e o conteúdo da biblioteca selecionada. É possível exibir o relatório e outros itens na biblioteca, explorar pastas e pesquisar o site para localizar itens.  
  
 Para distinguir os itens do servidor de relatório de outros itens em um site do SharePoint, você pode usar o ícone para identificar visualmente um item ou colocar pausar cursor do mouse sobre o tipo e ler a extensão do arquivo. A imagem a seguir mostra pastas e uma definição de relatório na biblioteca **Relatórios**:  
  
 ![Biblioteca do Sharepoint com itens do servidor de relatório](../../reporting-services/report-builder/media/rs-sharepointlibrary.gif "Biblioteca do Sharepoint com itens do servidor de relatório")  
  
### <a name="viewing-reports"></a>Exibindo relatórios  
 As definições de relatório (arquivos .rdl) que você carrega em uma biblioteca do SharePoint são exibidas através de uma Web Part do Visualizador de Relatórios que é instalada pelo Suplemento Reporting Services. Uma associação do arquivo .rdl é definida automaticamente quando você instala o suplemento. Ao selecionar um relatório, ele é aberto automaticamente no Web Part. Depois que o relatório abrir, você poderá usar a barra de ferramentas do relatório incluída na Web Part para navegar em páginas, pesquisar, aplicar zoom e imprimir o relatório. A barra de ferramentas inclui a opção Exportar como Feed de Dados para exportar o relatório como um feed de dados Atom e um menu **Ações** com opções para imprimir, assinar e exportar o relatório em formatos diferentes como PDF, Word e Excel. No menu **Ações** , você também pode abrir o relatório no Construtor de Relatórios. A imagem a seguir mostra um relatório e as opções de Opções de exportação no menu **Ação** .  
  
 ![rs_SharePointRunReport](../../reporting-services/report-builder/media/rs-sharepointrunreport.gif "rs_SharePointRunReport")  
  
### <a name="managing-items-through-actions"></a>Gerenciando itens por meio de ações  
 As tarefas de gerenciamento têm suporte por meio das ações em um menu suspenso para cada item. Dependendo de suas permissões, cada item tem ações comuns que são padrão para todos os itens que estão armazenados em uma biblioteca do SharePoint. **Exibir Propriedades** e **Editar Propriedades** são exemplos de ações comuns. Ações personalizadas fornecem uma funcionalidade de gerenciamento específica para os itens. A imagem a seguir mostra as ações para uma definição de relatório. Exemplos de ações personalizadas para uma definição de relatório incluem **Gerenciar Assinaturas** e **Gerenciar Opções de Processamento**:  
  
 ![Comandos de menu para itens de servidor de relatório](../../reporting-services/report-builder/media/rs-ecbforrsitems.gif "Comandos de menu para itens de servidor de relatório")  
  
  
##  <a name="viewing-reports-in-a-desktop-application"></a><a name="DeskTop"></a> Exibindo os relatórios em um aplicativo da área de trabalho  
 Você pode ignorar totalmente a exibição do navegador e usar um aplicativo da área de trabalho (como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) como visualizador de relatórios. Para fazer isso, defina uma assinatura que especifica um formato de aplicativo de desktop e um destino de pasta compartilhado. O servidor de relatório gera seu relatório como um arquivo de aplicativo, anexa uma extensão de nome de arquivo e salva o relatório como um arquivo em seu disco rígido. Você pode usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel (ou outro aplicativo) em vez de um navegador para exibir seu relatório.  
  
  
##  <a name="about-user-sessions"></a><a name="AboutUserSessions"></a> Sobre as sessões de usuário  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa sessões de navegador para manter a consistência enquanto exibe relatórios. As sessões se baseiam em conexões do navegador, não em usuários autenticados. Uma sessão nova é criada toda vez que um usuário abre um relatório em uma nova janela de navegador. Assim que uma sessão de navegador é estabelecida, você continua a trabalhar com a versão do relatório que foi aberta quando a sessão começou, mesmo que o relatório seja modificado no servidor de relatório. Por exemplo, se você abrir um relatório às 23 horas e um autor de relatório publicar novamente o mesmo relatório às 23h01, sua sessão conterá a versão que você abriu para a duração da sessão.  
  
 Se você atualizar um relatório na mesma sessão usando o botão **Atualizar** do navegador, a versão da sessão original do relatório será exibida. Se você atualizar um relatório sob demanda usando o botão **Atualizar** na barra de ferramentas do relatório, o relatório será executado novamente e novos dados, se houver, serão exibidos.  
  
 As informações da sessão são armazenadas no banco de dados temporário do servidor de relatório. O servidor de relatório não usa o gerenciamento de sessão [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Se você reinicializar o servidor ou executar uma operação de recuperação de banco de dados, o estado de sessão não será restaurado. Para obter mais informações sobre o gerenciamento de sessões, consulte [Identificando o estado de execução](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).  
  
 
##  <a name="in-this-section"></a><a name="InThisSection"></a> Nesta seção  
 Os artigos a seguir fornecem informações adicionais sobre como exibir e gerenciar relatórios.  
  
 [Encontrar, exibir e gerenciar relatórios](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
  
 [Localizando e exibindo relatórios com um navegador &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md)  
 Descreve como usar uma URL para localizar e exibir um relatório.  
  
 [Visualizar relatórios no Construtor de Relatórios](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)  
 Descreve como visualizar relatórios durante sua criação ou atualização.  
  
## <a name="see-also"></a>Confira também  
 [Salvando relatórios &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)   
 [Construtor de Relatórios no SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 