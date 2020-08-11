---
title: O portal da Web de um servidor de relatório (modo nativo) | Microsoft Docs
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: O portal da Web de um servidor de relatório do Reporting Services é uma experiência baseada na Web para exibição de relatórios, relatórios móveis e KPIs, bem como para navegação por meio dos elementos em sua instância do servidor de relatório.
ms.topic: conceptual
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29181b0830ad767c71e73c709aa7f3eee5a49190
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759794"
---
# <a name="the-web-portal-of-a-report-server-ssrs-native-mode"></a>O portal da Web de um servidor de relatório (modo nativo do SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

O portal da Web de um servidor de relatório do Reporting Services é uma experiência baseada na Web. No portal, você pode exibir relatórios, relatórios móveis e KPIs e navegar por elementos na instância do servidor de relatório. Você também pode usar o portal da Web para administrar uma única instância do servidor de relatório.

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>O que é o portal da Web

Você pode utilizar o portal da Web para executar as seguintes tarefas:

- Exibir, pesquisar, imprimir e assinar os relatórios.
- Criar, proteger e manter a hierarquia de pastas para organizar itens no servidor.
- Configure a segurança baseada em função que determina o acesso a itens e operações. Confira as [Definições de função – funções predefinidas](security/role-definitions-predefined-roles.md) para obter mais detalhes.
- Configurar propriedades de execução de relatório, histórico de relatórios e parâmetros de relatório.
- Criar agendas compartilhadas e fontes de dados compartilhadas para tornar as agendas e as conexões de fonte de dados mais gerenciáveis.
- Criar assinaturas controladas por dados que distribuem relatórios para uma grande lista de destinatários.
- Criar relatórios vinculados para reutilizar e redefinir o propósito de um relatório existente de diferentes maneiras.
- Baixar ferramentas comuns, como o Construtor de Relatórios e o Publicador de Relatórios Móveis.
- [Criar KPIs](../reporting-services/working-with-kpis-in-reporting-services.md).
- Enviar comentários ou fazer solicitações de recursos.

Você pode usar o portal da Web para navegar pelas pastas do servidor de relatório ou pesquisar relatórios específicos. É possível exibir um relatório, suas propriedades gerais e cópias antigas do relatório que são capturadas no histórico de relatórios. Dependendo de suas permissões, você também pode assinar relatórios para serem entregues em uma caixa de entrada de email ou pasta compartilhada no sistema de arquivos.

> [!NOTE]
> Para saber mais sobre navegadores e versões compatíveis, confira [Planning for Reporting Services Browser Support](../reporting-services/browser-support-for-reporting-services-and-power-view.md)(Planejar o suporte ao navegador do Reporting Services).

O portal da Web é usado apenas para um servidor de relatório executado no modo nativo. Ele não possui suporte para um servidor de relatório configurado no modo integrado do SharePoint.

Alguns recursos do portal da Web só estão disponíveis em edições específicas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, confira [Recursos do Reporting Services compatíveis com as Edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

Em uma nova instalação, somente os administradores locais têm permissões suficientes para trabalhar com o conteúdo e as configurações. Para conceder permissões a outros usuários, o administrador local deve criar atribuições de função que fornecem acesso ao servidor de relatório. As páginas de aplicativo e as tarefas que um usuário pode acessar posteriormente dependem das atribuições de função do usuário em questão. Para obter mais informações, consulte [Conceder acesso ao usuário a um servidor de relatório](security/grant-user-access-to-a-report-server-report-manager.md)

> [!NOTE]
> Se você estiver navegando para o portal da Web no computador local em que o servidor está em execução, será exibida uma mensagem indicando que você não tem permissão para exibir essa pasta. Isso se deve ao UAC (Controle de Acesso Universal) e ao fato de que você não está executando o navegador como um administrador. Não é possível executar o Microsoft Edge como um administrador. Você precisará usar o Internet Explorer. É possível navegar até o servidor remotamente ou iniciar o Internet Explorer como administrador e navegar até o portal da Web. Se quiser usar o portal da Web remotamente, você precisará conceder direitos de pasta ao gerenciador de conteúdo da sua conta.  

## <a name="start-and-use-the-web-portal"></a>Iniciar e usar o portal da Web

O portal da Web é um aplicativo Web que você abre digitando a URL do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] na barra de endereços em uma janela do navegador. Quando você iniciar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], as páginas, os links e as opções exibidas variarão de acordo com as permissões que você tem no servidor de relatório. Para executar uma tarefa, você deve estar atribuído a uma função que inclua a tarefa.  Um usuário que é atribuído a uma função que possui permissões totais tem acesso ao conjunto completo de menus e páginas de aplicativo disponíveis para gerenciar um servidor de relatório. Um usuário atribuído a uma função que possui permissões totais para exibir e executar relatórios vê apenas os menus e páginas que oferecem suporte a essas atividades. Cada usuário pode ter diferentes atribuições de função para diferentes servidores de relatório ou mesmo para diversos relatórios e pastas armazenados em um único servidor de relatório.

Para saber mais sobre funções, confira [Concedendo permissões em um servidor de relatório no modo nativo](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).

### <a name="start-the-web-portal"></a>Para iniciar o portal da Web

Para iniciar o portal da Web em um navegador, siga estas etapas:

1. Abra o navegador da Web. Para obter uma lista de navegadores da Web compatíveis, confira [Planning for Reporting Services Browser Support](../reporting-services/browser-support-for-reporting-services-and-power-view.md)(Planejando o suporte ao navegador do Reporting Services).

2. Na barra de endereços do navegador da Web, digite a URL do portal da Web.

    Por padrão, a URL é *https://[NomeDoComputador]/reports*.

    O servidor de relatório pode estar configurado para usar uma porta específica. Por exemplo *https://[NomeDoComputador]:80/reports* ou *https://[NomeDoComputador]:8080/reports*.

## <a name="grouping-by-categories"></a>Agrupando por categorias

O portal da Web agrupará os itens em diferentes categorias. As categorias disponíveis incluem:

- KPIs
- Relatórios móveis
- Relatórios paginados
- Relatórios do Power BI Desktop
- Pastas de trabalho do Excel
- Conjunto de dados
- Fontes de dados
- Recursos

Você pode controlar o que é exibido selecionando **Exibir** no canto superior direito. Se você selecionar Mostrar Ocultos, esses itens serão exibidos em uma cor mais clara.

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Relatórios do Power BI Desktop e pastas de trabalho do Excel

Carregue, organize e gerencie permissões para relatórios do Power BI Desktop e pastas de trabalho do Excel. Eles serão agrupados juntas no portal da Web.

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

Os arquivos são armazenados no Reporting Services, semelhante a outros arquivos de recurso. Selecionar um desses itens os baixará localmente no desktop. Salve as alterações feitas quando recarregá-las no servidor de relatório.

## <a name="search-for-items"></a>Pesquisar itens

Insira um termo de pesquisa e veja tudo o que você pode acessar. Os resultados são categorizados em KPIs, relatórios, conjuntos de dados e outros itens. Desse modo, você pode interagir com os resultados e adicioná-los aos seus favoritos.

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>Tarefas do portal da Web

[Identidade visual do portal da Web](../reporting-services/branding-the-web-portal.md)

[Como trabalhar com KPIs](../reporting-services/working-with-kpis-in-reporting-services.md)

[Working with shared datasets (Trabalhando com conjuntos de dados compartilhados)](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>Confira também

[Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[Configurar um URL (Gerenciador de configurações SSRS)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Ferramentas do Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
[Planning for Reporting Services Browser Support](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Recursos do Reporting Services compatíveis com as edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

Mais perguntas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
