---
title: Configurar um servidor de relatório no modo nativo para a Administração Local (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d1725e49ce825d3d57a3b41857e26a3843fbfc7c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104185"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>Configurar um servidor de relatório no modo nativo para a Administração Local (SSRS)
  A implantação de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um dos seguintes sistemas operacionais exigirá mais etapas de configuração se você desejar administrar localmente a instância do servidor de relatório. Este tópico explica como configurar o servidor de relatório para administração local. Se você ainda não instalou ou configurou o servidor de relatório, consulte [instalar SQL Server 2014 no assistente de instalação &#40;a instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) e [gerenciar um servidor de relatório no modo nativo do Reporting Services](manage-a-reporting-services-native-mode-report-server.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 Como o sistema operacional destacado limita as permissões, os membros do grupo Administradores local executam a maioria dos aplicativos como se estivessem usando a conta de Usuário Padrão.  
  
 Embora essa prática melhore a segurança geral do sistema, ela impede que você use as atribuições de funções internas predefinidas que o Reporting Services cria para administradores locais.  
  
-   [Visão geral de alterações de configuração](#bkmk_configuraiton_overview)  
  
-   [Para configurar um Servidor de Relatório Local e uma Administração do Gerenciador de Relatórios](#bkmk_configure_local_server)  
  
-   [Para configurar o SQL Server Management Studio (SSMS) para a administração de servidor de relatórios local](#bkmk_configure_ssms)  
  
-   [Para configurar o SQL Server Data Tools BI (SSDT) para publicar um Servidor de Relatórios Local](#bkmk_configure_ssdt)  
  
-   [Informações adicionais](#bkmk_addiitonal_informaiton)  
  
##  <a name="overview-of-configuration-changes"></a><a name="bkmk_configuraiton_overview"></a>Visão geral das alterações de configuração  
 As seguintes alterações de configuração configuram o servidor para que você possa usar permissões de usuário padrão para gerenciar o conteúdo e as operações do servidor de relatório:  
  
-   Adicione URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a sites confiáveis. Por padrão, o Internet Explorer que é executado nos sistemas operacionais listados é executado no **Modo Protegido**, um recurso que impede que solicitações do navegador alcancem processos de nível superior executados no mesmo computador. Você pode desabilitar o modo protegido para os aplicativos do servidor de relatório adicionando-os como Sites Confiáveis.  
  
-   Crie atribuições de função que concedam a você, o administrador do servidor de relatório, permissão para gerenciar o conteúdo e as operações, sem precisar usar o recurso **Executar como administrador** no Internet Explorer. Ao criar atribuições de funções para sua conta de usuário do Windows, você obtém acesso a um servidor de relatório com permissões de Gerenciador de Conteúdo e Administrador do Sistema por meio de atribuições explícitas de funções que substituem as atribuições de funções internas predefinidas que o Reporting Services cria.  
  
##  <a name="to-configure-local-report-server-and-report-manager-administration"></a><a name="bkmk_configure_local_server"></a>Para configurar o servidor de relatório local e a administração do Report Manager  
 Conclua as etapas de configuração nessa seção se você estiver navegando para um servidor de relatórios local e vir erros semelhantes ao seguinte:  
  
-   O usuário `'Domain\[user name]`' não tem as permissões necessárias. Verifique se as permissões suficientes foram concedidas e as restrições do UAC (Controle da conta de usuário) do Windows foram resolvidas.  
  
###  <a name="trusted-site-settings-in-the-browser"></a><a name="bkmk_site_settings"></a>Configurações de site confiáveis no navegador  
  
1.  Abra uma janela do navegador com permissões Executar como administrador. No menu **Iniciar** , clique em **Todos os Programas**, clique com o botão direito do mouse em **Internet Explorer**e selecione **Executar como administrador**.  
  
2.  Clique em **Permitir** para continuar.  
  
3.  No endereço da URL, insira a URL do Gerenciador de Relatórios. Para obter instruções, consulte [Gerenciador de Relatórios &#40;modo nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md) em Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Clique em **Ferramentas**.  
  
5.  Clique em **Opções da Internet**.  
  
6.  Clique em **Segurança**.  
  
7.  Clique em **Sites Confiáveis**.  
  
8.  Clique em **Sites**.  
  
9. Adicione `http://<your-server-name>`.  
  
10. Desmarque a caixa de seleção **Exigir certificação do servidor (https:) para todos os sites desta zona** se não estiver usando HTTPS para o site padrão.  
  
11. Clique em **Adicionar**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="report-manager-folder-settings"></a><a name="bkmk_configure_folder_settings"></a> Configurações da pasta do Gerenciador de Relatórios  
  
1.  No Gerenciador de Relatórios, na página inicial, clique em **Configurações de Pasta**.  
  
2.  Na página Configurações de Pasta, clique em **Segurança**.  
  
3.  Clique em **Atribuição de Nova Função**.  
  
4.  No campo **Nome do grupo ou do usuário** , conta de usuário do Windows neste formato: `<domain>\<user>`.  
  
5.  Selecione **Gerenciador de Conteúdo**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="report-manager-site-settings"></a><a name="bkmk_configure_site_settings"></a> Configurações do Site do Gerenciador de Relatórios  
  
1.  Abra seu navegador com privilégios administrativos e navegue até o gerenciador de relatórios, `http://<server name>/reports`.  
  
2.  Clique em **Configurações de Site** no canto superior da Página Inicial.  
  
    > [!TIP]  
    >  **Observação:** se a opção **Configurações de Site** não for exibida, feche e reabra o navegador, e navegue até o gerenciador de relatórios com privilégios administrativos.  
  
3.  Clique em **segurança**.  
  
4.  Clique em **Atribuição de Nova Função**.  
  
5.  No campo **Nome do grupo ou do usuário** , conta de usuário do Windows neste formato: `<domain>\<user>`.  
  
6.  Selecione **Administrador do Sistema**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Feche o Gerenciador de Relatórios.  
  
9. Abra novamente o Gerenciador de Relatórios no Internet Explorer sem usar **Executar como administrador**.  
  
##  <a name="to-configure-sql-server-management-studio-ssms-for-local-report-server-administration"></a><a name="bkmk_configure_ssms"></a>Para configurar o SQL Server Management Studio (SSMS) para a administração do servidor de relatório local  
 Por padrão, você não pode acessar todas as propriedades do servidor de relatório disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] a menos que inicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com privilégios administrativos.  
  
 **Para configurar as atribuições de função do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** , você não precisa iniciar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com permissões elevadas a cada vez:  
  
-   No menu **Iniciar** , clique em **Todos os Programas**, clique em **SQL Server 2014**, clique com o botão direito do mouse em **[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** e clique em **Executar como administrador**.  
  
-   Conecte-se ao servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] local.  
  
-   No nó **Segurança** , clique em **Funções do Sistema**.  
  
-   Clique com o botão direito do mouse em **Administrador do Sistema** e clique em **Propriedades**.  
  
-   Na página **Propriedades de Função do Sistema** , selecione **Exibir propriedades do servidor de relatório**. Selecione as outras propriedades que você quer associar aos membros da função administradores do sistema.  
  
-   Clique em **OK**.  
  
-   Feche o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Para adicionar um usuário à função do sistema "administrador do sistema", consulte a seção [Configurações do Site do Gerenciador de Relatórios](#bkmk_configure_site_settings) anteriormente neste tópico.  
  
 Agora, quando você abre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e não seleciona explicitamente **Executar como administrador** , tem acesso às propriedades do servidor de relatório.  
  
##  <a name="to-configure-sql-server-data-tools-bi-ssdt-to-publish-to-a-local-report-server"></a><a name="bkmk_configure_ssdt"></a>Para configurar o BI de SQL Server Data Tools (SSDT) para publicar em um servidor de relatório local  
 Se você instalou o [!INCLUDE[SSDTDev11](../../includes/ssdtdev11-md.md)] em um dos sistemas operacionais listados na primeira seção desse tópico, e quiser que o SSDT interaja com um servidor de relatório de modo Nativo local, receberá erros de permissão a menos que abra o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] com permissões elevadas ou configure as funções de serviços de relatório. Por exemplo, se você não tiver permissões adequadas, terá problemas semelhantes aos seguintes:  
  
-   Quando você tentar implantar itens de relatório no servidor de relatório local, verá uma mensagem de erro semelhante à seguinte na janela **Lista de Erros** :  
  
    -   As permissões concedidas ao usuário 'Domain\\<nome de usuário\>' são insuficientes para a execução dessa operação.  
  
 **Para executar com permissões elevadas a cada vez que você abrir o SSDT:**  
  
1.  Na tela iniciar, digite `sql server` e clique com o botão direito do mouse em **SQL Server Data Tools para Visual Studio**. Clique em **Executar como administrador**  
  
     **Ou**em sistemas operacionais mais antigos:  
  
     No menu **Iniciar** , clique em **Todos os Programas**, clique em **SQL Server 2014**, clique com o botão direito do mouse em **Ferramentas de Dados do SQL Server**e clique em **Executar como administrador**.  
  
2.  Clique em **Continuar**.  
  
3.  Clique em **Executar Programa**.  
  
 Agora você deve poder implantar relatórios e outros itens em um servidor de relatório local.  
  
 **Para configurar as atribuições de função do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você não precisa iniciar o SSDT com permissões elevadas a cada vez:**  
  
-   Consulte as seções [Configurações da pasta do Gerenciador de Relatórios](#bkmk_configure_folder_settings) e [Configurações do Site do Gerenciador de Relatórios](#bkmk_configure_site_settings) anteriormente neste tópico.  
  
##  <a name="additional-information"></a><a name="bkmk_addiitonal_informaiton"></a>Informações adicionais  
 Uma etapa de configuração adicional e comum relacionada à administração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é abrir a porta 80 no Windows Firewall para permitir o acesso ao computador do servidor de relatório. Para obter instruções, consulte [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](manage-a-reporting-services-native-mode-report-server.md)  
  
  
