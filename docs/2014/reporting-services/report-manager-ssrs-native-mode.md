---
title: Report Manager (modo nativo do SSRS) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 5cefc88469ac3c98f3bb944c0e490f1ce7e88472
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172359"
---
# <a name="report-manager--ssrs-native-mode"></a>Gerenciador de Relatórios (modo nativo do SSRS)
  O Gerenciador de Relatórios é uma ferramenta de gerenciamento e acesso a relatório com base na Web que é usada para administrar uma única instância de servidor de relatório a partir de um local remoto em uma conexão HTTP. Você também pode usar o Gerenciador de Relatórios para seu visualizador de relatório e recursos de navegação. Neste tópico:

-   [O que é o Gerenciador de Relatórios?](#bkmk_whatis_report_manager)

-   [Iniciar e usar o Gerenciador de Relatórios](#bkmk_start_report_manager)

-   [Descrições de ícones](#bkmk_icon_descriptions)

##  <a name="what-is-report-manager"></a><a name="bkmk_whatis_report_manager"></a>O que é Report Manager?
 É possível usar o Gerenciador de Relatórios para executar as seguintes tarefas:

-   Exibir, pesquisar, imprimir e assinar os relatórios.

-   Criar, proteger e manter a hierarquia de pastas para organizar itens no servidor.

-   Configure a segurança baseada em função que determina o acesso a itens e operações.

-   Configurar propriedades de execução de relatório, histórico de relatórios e parâmetros de relatório.

-   Crie modelos de relatório que se conectam e recuperam [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dados de uma fonte de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dados ou de uma fonte de dados relacional.

-   Definir a segurança do item de modelo para permitir acesso a entidades específicas no modelo ou mapear entidades para relatórios de clickthrough predefinidos que você cria com antecedência.

-   Criar agendas compartilhadas e fontes de dados compartilhadas para tornar as agendas e as conexões de fonte de dados mais gerenciáveis.

-   Criar assinaturas dirigidas aos dados que distribuem relatórios para uma grande lista de destinatários.

-   Criar relatórios vinculados para reutilizar e redefinir o propósito de um relatório existente de diferentes maneiras.

-   Iniciar o Construtor de Relatórios para criar relatórios que você possa salvar e executar no servidor de relatório.

 Você pode usar o Gerenciador de Relatórios para navegar pelas pastas do servidor de relatório ou pesquisar relatórios específicos. É possível exibir um relatório, suas propriedades gerais e cópias antigas do relatório que são capturadas no histórico de relatórios. Dependendo de suas permissões, você também pode assinar relatórios para serem entregues em uma caixa de entrada de email ou pasta compartilhada no sistema de arquivos.

> [!NOTE]
>  Para obter informações sobre navegadores e versões com suporte, consulte [planejamento para Reporting Services e suporte ao navegador de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).

 O Gerenciador de Relatórios só é usado para um servidor de relatório executado no modo nativo. Ele não possui suporte para um servidor de relatório configurado no modo integrado do SharePoint.

 Alguns recursos do Gerenciador de Relatórios só estão disponíveis em edições específicas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).

 Em uma nova instalação, somente os administradores locais têm permissões suficientes para trabalhar com o conteúdo e as configurações. Para conceder permissões a outros usuários, o administrador local deve criar atribuições de função que fornecem acesso ao servidor de relatório. As páginas de aplicativo e as tarefas que um usuário pode acessar posteriormente dependem das atribuições de função do usuário em questão. Para obter mais informações, consulte [conceder acesso de usuário a um servidor de relatório &#40;Report Manager&#41;](security/grant-user-access-to-a-report-server.md).

 Se você estiver usando o [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] ou o Windows Server 2008, configure o Gerenciador de Relatórios para administração local. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

##  <a name="start-and-use-report-manager"></a><a name="bkmk_start_report_manager"></a>Iniciar e usar o Report Manager
 O Gerenciador de Relatórios é um aplicativo Web que você abre digitando a URL do Gerenciador de Relatórios na barra de endereços de uma janela de navegador. Ao iniciar o Gerenciador de Relatórios, as páginas, links e opções exibidas variam com base nas permissões que você possui do servidor de relatório. Para executar uma tarefa, você deve estar atribuído a uma função que inclua a tarefa. Um usuário que é atribuído a uma função que possui permissões totais tem acesso ao conjunto completo de menus e páginas de aplicativo disponíveis para gerenciar um servidor de relatório. Um usuário atribuído a uma função que possui permissões totais para exibir e executar relatórios vê apenas os menus e páginas que oferecem suporte a essas atividades. Cada usuário pode ter diferentes atribuições de função para diferentes servidores de relatório ou mesmo para diversos relatórios e pastas armazenados em um único servidor de relatório.

 Para saber mais sobre funções, confira [Concedendo permissões em um servidor de relatório no modo nativo](security/granting-permissions-on-a-native-mode-report-server.md).

> [!NOTE]
>  Se você estiver usando o Windows Vista ou o Windows Server 2008, deverá configurar o servidor de relatórios para administração local antes de poder usar o Gerenciador de Relatórios para gerenciar uma instância do servidor de relatórios local. Para obter instruções sobre como configurar o servidor, consulte [configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

## <a name="start-report-manager"></a>Iniciar o Gerenciador de Relatórios

#### <a name="to-start-report-manager-from-a-browser"></a>Para iniciar o Gerenciador de Relatórios em um navegador

1.  Abra o [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 ou posterior.

2.  Na barra de endereço do navegador da Web, digite a URL do Gerenciador de Relatórios.

    -   Por padrão, a URL é `http://[ComputerName]/reports`.

    -   O servidor de relatório pode estar configurado para usar uma porta específica. Por exemplo, `http:// [ComputerName]:80/reports` ou `http:// [ComputerName]:8080/reports`.

## <a name="configuring-report-manager"></a>Configurando o Gerenciador de Relatórios
 A configuração do Gerenciador de Relatórios consiste em definir uma URL para o aplicativo. Uma configuração adicional será necessária se sua implantação incluir a execução do Gerenciador de Relatórios em um computador separado.

 É possível personalizar o Gerenciador de Relatórios de maneiras muito limitadas. Por exemplo, você pode modificar o título do aplicativo na página Configurações de Site. Se você for um desenvolvedor Web, poderá modificar as folhas de estilo que contêm as informações de estilo usadas pelo Gerenciador de Relatórios. Como o Gerenciador de Relatórios não foi criado especificamente para aceitar personalização, é necessário testar extensivamente qualquer modificação que você faça. Se você achar que o Gerenciador de Relatórios não atende às suas necessidades, poderá desenvolver um visualizador de relatórios personalizado ou configurar Web Parts do SharePoint para localizar e exibir relatórios em um site do SharePoint. Para obter mais informações, consulte [Configurar o Gerenciador de Relatórios &#40;Modo Nativo&#41;](report-server/configure-web-portal.md).

##  <a name="icon-descriptions"></a><a name="bkmk_icon_descriptions"></a>Descrições de ícones
 A tabela a seguir descreve os ícones usados no Gerenciador de Relatórios. Para obter mais informações sobre os ícones que aparecem na barra de ferramentas de relatório, consulte [Visualizador de HTML e a barra de ferramentas de relatório](html-viewer-and-the-report-toolbar.md).

|ícone|Descrição|Ação|
|----------|-----------------|------------|
|![Ícone do relatório](media/hlp-16doc.gif "Ícone do relatório")|Relatório|Clique no nome ou no ícone do relatório para abrir o relatório. O relatório é aberto em uma janela separada.|
|![Ícone de modelo](media/model-icon.gif "Ícone de modelo")|Modelo de relatório|Clique no ícone do modelo de relatório para abrir páginas de propriedades do modelo.|
|![Ícone do relatório vinculado](media/hlp-16linked.gif "Ícone do relatório vinculado")|Relatório vinculado|Clique no ícone do relatório ou nome para abrir o relatório vinculado. O relatório é aberto em uma janela separada.|
|![Ícone de pasta](media/hlp-16folder.gif "Ícone de pasta")|Pasta|Clique no nome ou no ícone da pasta para abrir a pasta.|
|![Ícone de assinatura](media/hlp-16subscription.gif "Ícone de assinatura")|Subscription|Clique em um ícone ou descrição de assinatura para editar uma assinatura.|
|![Ícone de assinatura controlada por dados](media/hlp-16subscriptiondd.gif "Ícone de assinatura controlada por dados")|Assinatura controlada por dados|Clique em um ícone ou descrição de assinatura controlada por dados para editar uma assinatura.|
|![ícone de recurso genérico](media/hlp-16file.gif "ícone de recurso genérico")|Recurso|Clique no nome ou no ícone do recurso para abrir o recurso. O recurso é aberto em uma janela separada.|
|![Ícone da fonte de dados compartilhada](media/hlp-16datasource.png "Ícone da fonte de dados compartilhada")|Item de fonte de dados compartilhada|Clique em um ícone de fonte de dados compartilhada para abrir a página de propriedades, lista de relatório e lista de assinatura da fonte de dados.|
|![Ícone de página de propriedades](media/hlp-16prop.gif "Ícone de página de propriedades")|Página Propriedades|Clique no ícone de propriedade para acessar páginas adicionais e definir propriedades e segurança.|

## <a name="see-also"></a>Confira também

- [Configurar uma URL &#40;SSRS Configuration Manager&#41;](install-windows/configure-a-url-ssrs-configuration-manager.md)
- [Planejamento para Reporting Services e suporte ao navegador de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [Construtor de Relatórios &#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)
- - [Ferramentas de Reporting Services](tools/reporting-services-tools.md)
- [Gerenciamento de conteúdo do servidor de relatório &#40;modo nativo do SSRS&#41;](report-server/report-server-content-management-ssrs-native-mode.md) 
 [ajuda de F1 do Report Manager](../../2014/reporting-services/report-manager-f1-help.md)