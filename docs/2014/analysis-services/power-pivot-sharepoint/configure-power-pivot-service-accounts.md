---
title: Configurar contas de serviço PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
author: minewiskan
ms.author: owend
ms.openlocfilehash: d4053c7a15d0131773b72f347caab7cbc42d6044
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547528"
---
# <a name="configure-powerpivot-service-accounts"></a>Configurar contas de serviço PowerPivot
  Uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] inclui dois serviços que oferecem suporte a operações de servidor. O **SQL Server Analysis Services (PowerPivot)** é um serviço do Windows que fornece processamento de dados PowerPivot e suporte a consultas em um servidor de aplicativos. A conta de logon desse serviço sempre é especificada durante a Instalação do SQL Server, quando você instala o Analysis Services no modo integrado do SharePoint.  
  
 Uma segunda conta deve ser especificada para o aplicativo de serviço PowerPivot, um serviço Web compartilhado executado sob uma identidade de pool de aplicativos em um farm do SharePoint. Essa conta é especificada quando você configura uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] usando a ferramenta de Configuração do PowerPivot ou PowerShell.  
  
 Cada serviço deve ser executado sob uma conta dedicada de forma que você possa auditar as conexões ou habilitar o protocolo de autenticação Kerberos no farm.  
  
 Uma vez definidas as contas de serviço, as alterações em qualquer uma delas deverão ser feitas através da Administração Central do SharePoint. Se você usar ferramentas alternativas (como o aplicativo de console Serviços, o Gerenciador do IIS ou o SQL Server Configuration Manager), as permissões não serão atualizadas para acesso a banco de dados no farm ou para acesso a arquivo local no servidor físico.  
  
 Este tópico contém as seguintes seções:  
  
 [Atualizar uma senha expirada para instância do SQL Server Analysis Services (PowerPivot)](#bkmk_passwordssas)  
  
 [Atualizar uma senha expirada para o aplicativo de serviço PowerPivot](configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [Alterar a conta sob a qual cada serviço é executado](#bkmk_newacct)  
  
 [Criar ou alterar o pool de aplicativos para um aplicativo de serviço PowerPivot](#bkmk_appPool)  
  
 [Requisitos e permissões de conta](#requirements)  
  
 [Solucionando problemas: Conceder permissões administrativas manualmente](#updatemanually)  
  
 [Solucionando problemas: resolver erros HTTP 503 devido a senhas expiradas para Administração Central ou serviço do aplicativo Web do Microsoft SharePoint Foundation](#expired)  
  
##  <a name="update-an-expired-password-for-sql-server-analysis-services-powerpivot-instance"></a><a name="bkmk_passwordssas"></a>Atualizar uma senha expirada para a instância do SQL Server Analysis Services (PowerPivot)  
  
1.  Aponte para Iniciar, clique em **Ferramentas Administrativas**e em **Serviços**. Clique duas vezes em **SQL Server Analysis Services (PowerPivot)**. Clique em **Logon**e digite a nova senha da conta.  
  
2.  Na Administração Central, na seção Segurança, clique em **Configurar contas gerenciadas**.  
  
3.  Clique em **Editar** para alterar uma conta específica.  
  
4.  Selecione **Alterar senha agora**.  
  
5.  Selecione **Definir senha da conta com novo valor**. Todos os serviços que são executados sob a conta gerenciada usarão as credenciais atualizadas.  
  
##  <a name="update-an-expired-password-for-the-powerpivot-service-application"></a><a name="bkmk_passwordapp"></a>Atualizar uma senha expirada para o aplicativo de serviço PowerPivot  
  
1.  Na Administração Central, na seção Segurança, clique em **Configurar contas gerenciadas**.  
  
2.  Clique em **Editar** para alterar uma conta específica.  
  
3.  Selecione **Alterar senha agora**.  
  
4.  Selecione **Definir senha da conta com novo valor**. Todos os serviços que são executados sob a conta gerenciada usarão as credenciais atualizadas.  
  
##  <a name="change-the-account-under-which-each-service-runs"></a><a name="bkmk_newacct"></a>Alterar a conta na qual cada serviço é executado  
  
1.  Na Administração Central, na seção Segurança, clique em **Configurar contas de serviço**.  
  
2.  Selecione **Serviço Windows - SQL Server Analysis Services** para alterar a conta de serviço do Analysis Services.  
  
3.  Em **Selecione uma conta para esse serviço**, escolha uma conta gerenciada existente ou crie uma nova. A conta deve ser uma conta de usuário de domínio.  
  
4.  Selecione **Pool de Aplicativos de Serviço - Sistema de Serviços Web do SharePoint** para alterar a identidade do pool de aplicativos do aplicativo de serviço PowerPivot padrão. Dependendo em como sua instalação foi configurada, o serviço pode estar em execução sob um pool de aplicativos de serviço existente criado para os serviços do SharePoint. Por padrão, a Ferramenta de Configuração do PowerPivot registra o serviço como **Aplicativo de Serviço PowerPivot Padrão (Aplicativo de Serviço PowerPivot)**.  
  
     Se o serviço tiver sido configurado manualmente por um administrador do SharePoint, ele provavelmente terá seu próprio pool de aplicativos de serviço.  
  
5.  Em **Selecione uma conta para esse serviço**, escolha uma conta gerenciada existente ou crie uma nova. A conta deve ser uma conta de usuário de domínio.  
  
6.  Clique em **OK**.  
  
##  <a name="create-or-change-the-application-pool-for-a-powerpivot-service-application"></a><a name="bkmk_appPool"></a>Criar ou alterar o pool de aplicativos para um aplicativo de serviço PowerPivot  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
2.  Selecione, mas não clique, o aplicativo de serviço PowerPivot. Se você clicar no nome do aplicativo, o Painel de Gerenciamento PowerPivot será aberto, não oferecendo um link à página de propriedades que especifica o pool de aplicativos.  Você pode clicar no espaço em branco vazio na linha, ou clicar no nome do tipo, para selecionar o aplicativo de serviço PowerPivot.  
  
3.  Clique em **Propriedades** na faixa de opções.  
  
4.  Selecione **Criar um novo pool de aplicativos**. Forneça um nome para o pool de aplicativos e especifique uma conta gerenciada para sua identidade.  
  
##  <a name="account-requirements-and-permissions"></a><a name="requirements"></a>Requisitos e permissões da conta  
 O planejamento de uma implantação do PowerPivot para SharePoint deve incluir as contas de serviço a seguir.  
  
-   Conta de serviço do Analysis Services. O Analysis Services processa consultas do PowerPivot e trabalhos de atualização de dados no farm. Essa conta sempre é especificada durante a Instalação do SQL Server quando você instala PowerPivot para SharePoint.  
  
-   Pool de aplicativos do serviço PowerPivot. Um aplicativo do serviço PowerPivot está associado a um Serviço do Sistema PowerPivot que fornece a integração do SharePoint e a infraestrutura para o processamento de consultas do PowerPivot em um farm. O pool de aplicativos especificado para um aplicativo de serviço PowerPivot é a identidade de serviço do Serviço de Sistema PowerPivot. Você pode ter vários aplicativos do serviço PowerPivot em um farm. Cada aplicativo criado deve ser executado em seu próprio pool de aplicativos.  
  
#### <a name="analysis-services-service-account"></a>Conta de serviço do Analysis Services  
  
|Requisito|Descrição|  
|-----------------|-----------------|  
|Requisito de provisionamento|Essa conta deve ser especificada durante a instalação do SQL Server usando a **página de configuração Analysis Services** no assistente de instalação (ou o `ASSVCACCOUNT` parâmetro de instalação em uma configuração de linha de comando).<br /><br /> Você pode modificar o nome de usuário ou a senha usando a Administração Central, o PowerShell ou a Ferramenta de Configuração do PowerPivot. Não há suporte para o uso de outras ferramentas para alterar contas e senhas.|  
|Requisito da conta de usuário de domínio|Essa conta deve ser uma conta de usuário de domínio do Windows. São proibidas contas de máquinas internas (como Serviço de Rede ou Serviço Local). A Instalação do SQL Server impõe o requisito de conta de usuário de domínio bloqueando a instalação sempre que uma conta de computador é especificada.|  
|Requisitos de permissão|Essa conta deve ser membro do grupo de segurança SQLServerMSASUser $ \<server> $PowerPivot e dos grupos de segurança WSS_WPG no computador local. Essas permissões devem ser concedidas automaticamente. Para obter mais informações sobre como verificar ou conceder permissões, consulte [conceder as permissões administrativas da conta de serviço PowerPivot manualmente](#updatemanually) neste tópico e [configuração inicial &#40;PowerPivot para SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).|  
|Requisitos de expansão|Se você instalar várias instâncias de servidor do PowerPivot para SharePoint em um farm, todas as instâncias de servidor do Analysis Services deverão ser executadas sob a mesma conta de usuário de domínio. Por exemplo, se você configurar a primeira instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] para execução como Contoso\ssas-srv01, todas as instâncias do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] adicionais implantadas posteriormente no mesmo farm também deverão executar como Contoso\ssas-srv01 (ou qualquer que seja a conta atual).<br /><br /> A configuração de todas as instâncias de serviço para execução na mesma conta permite que o serviço Sistema PowerPivot aloque o processamento de consultas ou trabalhos de atualização de dados para qualquer instância de serviço do Analysis Services no farm. Além disso, ela habilita o uso do recurso Conta Gerenciada na Administração Central para instâncias de servidor do Analysis Services. Usando a mesma conta para todas as instâncias do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , você pode alterar a conta ou a senha uma vez, e todas as instâncias de serviço que usam essas credenciais são atualizadas automaticamente.<br /><br /> A Instalação do SQL Server impõe o requisito de mesma conta. Em uma implantação em expansão onde um farm do SharePoint já tem uma instância do PowerPivot para SharePoint instalada, a Instalação bloqueará a nova instalação se a conta do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] especificada for diferente de uma já em uso no farm.|  
  
#### <a name="powerpivot-service-application-pool"></a>Pool de aplicativos do serviço PowerPivot  
  
|Requisito|Descrição|  
|-----------------|-----------------|  
|Requisito de provisionamento|O Serviço do Sistema PowerPivot é um recurso compartilhado no farm que fica disponível quando você cria um aplicativo de serviço. O pool de aplicativos de serviço deve ser especificado quando o aplicativo de serviço é criado. Ele pode ser especificado de dois modos: usando a ferramenta de configuração do PowerPivot ou por comandos do PowerShell.<br /><br /> Você pode ter configurado a identidade do pool de aplicativos para executar sob uma conta exclusiva. Mas se você não fez isso, considere alterá-lo agora para ser executado em uma conta diferente.|  
|Requisito da conta de usuário de domínio|A identidade do pool de aplicativos deve ser uma conta de usuário de domínio do Windows. São proibidas contas de máquinas internas (como Serviço de Rede ou Serviço Local).|  
|Requisitos de permissão|Esta conta não precisa de permissões de Administrador do sistema local no computador. Entretanto, essa conta deve ter permissões de administrador de sistema do Analysis Services no [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] local instalado no mesmo computador. Essas permissões são concedidas automaticamente pela Instalação do SQL Server, ou quando você define ou altera a identidade de pool e aplicativos na Administração Central.<br /><br /> Permissões administrativas são necessárias para encaminhar consultas ao [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Elas também são necessárias para monitorar a integridade, fechar sessões inativas e escutar eventos de rastreamento.<br /><br /> A conta precisa ter permissões de conexão, leitura e gravação no banco de dados do aplicativo do serviço PowerPivot. Essas permissões são concedidas automaticamente quando o aplicativo é criado e são atualizadas automaticamente quando você altera as contas ou senhas na Administração Central.<br /><br /> O aplicativo de serviço PowerPivot verificará se um usuário do SharePoint está autorizado a exibir dados antes de recuperar o arquivo, mas ele não representa o usuário. Não há requisitos de permissão para representação.|  
|Requisitos de expansão|Nenhum.|  
  
##  <a name="troubleshooting-grant-administrative-permissions-manually"></a><a name="updatemanually"></a>Solução de problemas: conceder permissões administrativas manualmente  
 As permissões administrativas não atualizarão se a pessoa que atualiza as credenciais não for um administrador local no computador. Se isto ocorrer, você poderá conceder permissões administrativas manualmente. O modo mais fácil de fazer isto é executar o trabalho de timer de Configuração do PowerPivot na Administração Central. Com esta abordagem, você pode reiniciar permissões para todos os servidores do PowerPivot no farm. Observe que esta abordagem somente funcionará se o trabalho de timer do SharePoint estiver sendo executado como administrador de farm e como administrador local no computador.  
  
1.  Em Monitoração, clique em **Revisar definições de trabalho**.  
  
2.  Selecione **Trabalho de Timer da Configuração do PowerPivot**.  
  
3.  Clique em **executar agora**.  
  
 Como último recurso, você pode garantir as permissões corretas concedendo Analysis Services permissões de administração do sistema ao aplicativo de serviço PowerPivot e, em seguida, adicionar especificamente a identidade do aplicativo de serviço ao grupo de segurança do Windows SQLServerMSASUser $ \<servername> $PowerPivot. Você deve repetir estas etapas para cada instância do Analysis Services integrada com o farm do SharePoint.  
  
 Você deve ser um administrador local para atualizar grupos de segurança do Windows.  
  
1.  Em SQL Server Management Studio, conecte-se à instância de Analysis Services como \<server name> \powerpivot.  
  
2.  Clique com o botão direito do mouse no nome do servidor e selecione **Propriedades**.  
  
3.  Clique em **Segurança**.  
  
4.  Clique em **Adicionar**.  
  
5.  Digite o nome da conta que é usada para o pool de aplicativos do serviço PowerPivot e clique em **OK**.  
  
6.  Em Ferramentas Administrativas, clique em **Gerenciamento do Computador**.  
  
7.  Abra **Usuários e Grupos Locais**.  
  
8.  Abra **Grupos**.  
  
9. Clique duas vezes em SQLServerMSASUser $ \<servername> $PowerPivot.  
  
10. Clique em **Adicionar**.  
  
11. Digite o nome da conta que é usada para o pool de aplicativos do serviço PowerPivot e clique em **OK**.  
  
##  <a name="troubleshooting-resolve-http-503-errors-due-to-expired-passwords-for-central-administration-or-the-sharepoint-foundation-web-application-service"></a><a name="expired"></a>Solução de problemas: resolver erros de HTTP 503 devido a senhas expiradas para administração central ou serviço de aplicativo Web do SharePoint Foundation  
 Se o serviço da Administração Central ou o serviço do aplicativo Web do Microsoft SharePoint Foundation deixar de funcionar devido a uma redefinição de conta ou expiração de senha, você receberá a mensagem de erro HTTP 503 "Serviço não disponível" ao tentar abrir a Administração Central do SharePoint ou um site do SharePoint. Siga estas etapas para colocar o servidor online novamente. Quando a Administração Central estiver disponível, você poderá continuar atualizando informações de conta expiradas.  
  
1.  Em Ferramentas administrativas, clique em **Gerenciador dos Serviços de Informações da Internet**.  
  
2.  Para a identidade do site ou pool de aplicativos da Administração Central, se uma conta de usuário de domínio tiver uma senha expirada, faça o seguinte:  
  
    1.  Clique com o botão direito do mouse no nome do pool de aplicativos e selecione **Configurações Avançadas**.  
  
    2.  Selecione **identidade** e clique em... para abrir a caixa de diálogo identidade do pool de aplicativos.  
  
    3.  Clique em **Definir**.  
  
    4.  Digite o nome de usuário e a senha.  
  
3.  Execute IISRESET. Para fazer isto, abra um prompt de comando do Administrador e digite `iisreset` no comando.  
  
4.  Na Administração Central do SharePoint, em Segurança, selecione **Configurar contas gerenciadas**.  
  
5.  Clique em **Editar** para atualizar as informações da conta gerenciada que tem a senha expirada.  
  
6.  Selecione **Alterar senha agora**.  
  
7.  Clique em **Usar senha existente**.  
  
8.  Digite a senha e clique em **OK**.  
  
 Se o Reporting Services estiver instalado, use o Gerenciador de Configuração do Reporting Services para atualizar senhas para o servidor de relatório e a conexão para o banco de dados do servidor de relatórios. Para obter mais informações, consulte [Configuração e administração de um servidor de relatório &#40;modo do SharePoint do Reporting Services&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar ou parar um servidor de PowerPivot para SharePoint](start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Configurar a conta de atualização de dados autônoma do PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
  
