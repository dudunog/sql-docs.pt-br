---
title: Instalação e Configuração
description: Saiba como instalar o Master Data Services em um computador com o Windows Server 2012 R2, configurar o banco de dados e o site do MDS e implantar os modelos de exemplo e o Data.
ms.custom: ''
ms.date: 07/01/2020
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: quickstart
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 92511a835a8a9a6f899f7597900fec6707f6dada
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129426"
---
# <a name="master-data-services-installation-and-configuration"></a>Instalação e configuração do Master Data Services

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo aborda a instalação do [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em um computador com Windows Server 2012 R2, configuração do site e banco de dados do MDS e implantação dos dados e modelos de exemplo. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) permite que sua organização gerencie uma versão confiável dos dados.   
  
> [!NOTE] 
> Você pode instalar o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em um computador com Windows 10 quando usar a edição Developer que agora dá suporte para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. 
>>Para obter mais informações sobre o suporte ao sistema operacional para diferentes edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Requisitos de hardware e software para a instalação do SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). 

Para obter uma visão geral de como organizar dados no [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Visão geral do MDS (Master Data Services)](../master-data-services/master-data-services-overview-mds.md).     
  
 Para obter informações sobre os novos recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novidades do MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Para obter links para vídeos e outros recursos de treinamento para ajudá-lo a saber mais sobre o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Learn Master Data Services (Saiba mais sobre o Master Data Services)](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Download**  
> -   Para baixar o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)** .  
> -   Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)** para criar uma Máquina Virtual com o SQL Server já está instalado.  
> 
> **Não está conseguindo criar um site do MDS?**
> >Confira este artigo de suporte da Microsoft para obter instruções sobre como resolver esse problema.
> [Não é possível criar um site do MDS por meio de uma conta de baixo privilégio no SQL Server 2016](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Internet Explorer e Silverlight
- Quando você instala o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em um computador com Windows Server 2012, pode ser necessário configurar a Segurança Melhorada do Internet Explorer para permitir script para o site do aplicativo Web. Caso contrário, haverá falha ao navegar até o site de no computador de servidor.
- Para trabalhar no aplicativo Web, o Silverlight 5 deve estar instalado no computador cliente. Se você não tiver a versão exigida do Silverlight, será solicitado a instalá-la quando navegar até uma área do aplicativo Web que a exige. Você pode instalar o Silverlight 5 por **[aqui](https://www.microsoft.com/silverlight/)**.

## <a name="ssmdsshort_md-on-an-azure-virtual-machine"></a>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em uma máquina virtual do Azure
Por padrão, quando você cria uma máquina virtual do Azure com o [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] já instalado, o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] também é instalado. 

A próxima etapa é instalar o IIS (Serviços de Informações da Internet). Consulte a seção [Instalando e configurando o IIS](#InstallIIS). 

Se você estiver interessado em fazer alterações na instalação do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], encontrará o arquivo setup.exe no local padrão, `<drive>`:\SQLServer_13.0_Full.
  
## <a name="installing-master-data-services"></a><a name="InstallMDS"></a> Instalando o Master Data Services  
 Você usa o assistente de instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou um prompt de comando para instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
 **Para instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usando a Configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador Windows Server 2012 R2**  
  
1.  Clique duas vezes em Setup.exe e siga as etapas no assistente de instalação.  
  
2.  Selecione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] na página **Seleção de Recursos** em **Recursos Compartilhados**.  
  
     A opção instala o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], assemblies, um snap-in do Windows PowerShell, pastas e arquivos de aplicativos Web e serviços Web.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Conclua o assistente de instalação.  

## <a name="installing-and-configuring-iis"></a><a name="InstallIIS"></a> Instalando e configurando o IIS
  
1.  No [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)], clique no ícone **Gerenciador do Servidor** na barra de tarefas da **Área de Trabalho**.  
  
     ![Ícone para o Gerenciador do Servidor na barra de tarefas do Windows Server 2012](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Ícone para o Gerenciador do Servidor na barra de tarefas do Windows Server 2012")  
  
5.  Em **Gerenciador do Servidor**, clique em **Adicionar Funções e Recursos** no menu **Gerenciar** .  
   
     ![No servidor gerenciar, o comando de menu Adicionar funções e recursos](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "No servidor gerenciar, o comando de menu Adicionar funções e recursos")  
  
6.  Na página **Tipo de Instalação** do **Assistente para Adicionar Funções e Recursos**, aceite o valor padrão (**Instalação baseada em função ou em recurso**) e clique em **Avançar**.  
  
7.  Clique em **Selecionar um servidor no pool de servidores** e clique no servidor em que você instalou o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. Na página **Funções de Servidor**, clique em **Servidor Web** e clique em **Avançar**. 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. Na página **Recursos**, confirme se os recursos a seguir estão selecionados e clique em **Avançar**. Esses recursos são necessários para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)].
  
    |Recursos|Recursos|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. No painel esquerdo, clique em **Função de Servidor Web (IIS)** e, em seguida, clique em **Serviços de Função**.
11. Na página **Serviços de Função**, confirme se os serviços a seguir estão selecionados e clique em **Avançar**. Esses serviços são necessários para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] em [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)].

    > [!WARNING]  
    >  Não instale o serviço de função Publicação do WebDAV. Publicação do WebDAV não é compatível com o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     |Serviços de Função|Serviços de Função|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     Para obter uma lista dos recursos e dos serviços de funções necessários em outros sistemas operacionais, consulte [Requisitos do aplicativo Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).   
  
 Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a configuração, veja [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Configuração&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
 Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando um prompt de comando, consulte [Instalar o SQL Server 2016 por meio do prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md). Ao usar um prompt de comando, o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponível como um parâmetro de recurso.  
  
 Para obter uma descrição breve com links para mais informações sobre tarefas de pré-instalação, consulte [Instalar o Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="setting-up-the-database-and-website"></a><a name="SetUpWeb"></a> Configurar o banco de dados e o site  
 **Para configurar o banco de dados e o site usando o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]**  

 
> [!WARNING]
>  Você deve [instalar o IIS](#InstallIIS) antes de iniciar o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager. Caso contrário, o Configuration Manager exibirá um erro de Serviços de Informações da Internet e você não poderá criar o aplicativo Web [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)].  
> 
> **Requisitos do navegador**
> >O aplicativo Web [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] funciona apenas no Internet Explorer (IE) 9 ou posterior. Não há suporte para o IE 8 e versões anteriores, para o Microsoft Edge e o Chrome.    
  
1.  Inicie o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]e clique em **Configuração do Banco de Dados** no painel esquerdo.  
  
2.  Clique em **Criar Banco de Dados** e em **Avançar** no **Assistente para Criar Banco de Dados**.  
  
3.  Na página **servidor de banco de dados** , especifique a instância de SQL Server. 

    >  [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] Adiciona suporte para SQL Server Instância Gerenciada. Defina o valor de **SQL Server instância** como o host da instância gerenciada. Por exemplo, `xxxxxx.xxxxxx.database.windows.net`.

4. Selecione o **tipo de autenticação** e clique em **testar conexão** para confirmar que você pode se conectar ao banco de dados usando as credenciais para o tipo de autenticação selecionado. Clique em **Próximo**.

    >Para [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] o, para se conectar à instância gerenciada, use um dos seguintes tipos de autenticação:
    >
    >- Azure Active Directory autenticação integrada: **usuário atual – Active Directory integrado**
    >- Autenticação de SQL Server: **SQL Server conta**.
    >
    >No SQL Instância Gerenciada, o usuário deve ser um membro da `sysadmin` função de servidor fixa.

    > [!NOTE]  
    >  Quando você seleciona a **segurança atual integrada ao usuário** como o tipo de autenticação, a caixa **nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectada ao computador. Se você estiver executando o [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em uma VM (máquina Virtual) do Azure, a caixa **Nome de usuário** exibe o nome da VM e o nome de usuário para a conta de administrador local na VM. 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  Digite um nome no campo **Nome do banco de dados** . Opcionalmente, para selecionar uma ordenação do Windows, desmarque a caixa de seleção **Ordenação padrão do SQL Server** e clique em uma ou mais das opções disponíveis como **Diferenciar maiúsculas de minúsculas**. Clique em **Próximo**.

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Para obter mais informações sobre a ordenação do Windows, consulte [Nome de ordenação do Windows (Transact-SQL)](../t-sql/statements/windows-collation-name-transact-sql.md).  
  
5.  No campo **Nome de usuário** , especifique a conta do Windows do usuário que será o Superusuário padrão do Master Data Services. Um Superusuário tem acesso a todas as áreas funcionais e pode adicionar, excluir e atualizar todos os modelos.  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  Clique em **Avançar** para exibir um resumo das configurações do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] e em **Avançar** novamente para criar o banco de dados. A página **Progresso e Conclusão** é exibida.

7. Quando o banco de dados estiver criado e configurado, clique em **Concluir**.  
  
     Para obter mais informações sobre as configurações do **Assistente para Criar Banco de Dados**, consulte [Assistente para Criar Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  Na página **Configuração do Banco de Dados** do [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], clique em **Selecionar Banco de Dados**.  
  
8.  Clique em **Conectar**, selecione o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] criado na Etapa 7 e clique em **OK**. 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     Você terminou de configurar o banco de dados. A página **Configuração do Banco de Dados** agora exibe a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual você está conectado no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], o banco de dados criado e a versão atual do banco de dados.  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. Em [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], clique em **Configuração da Web** no painel esquerdo.  
  
10. Na caixa de listagem **Site** , clique em **Site Padrão** e em **Criar** para criar um aplicativo Web.  
  
    > [!NOTE]  
    >  Quando você seleciona **Site Padrão**, é necessário criar um aplicativo Web. Se você selecionar **Criar novo site** na caixa de listagem, o aplicativo será criado automaticamente.  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. Na seção **Pool de Aplicativos** , escolha uma das ações a seguir.  
  
    -   Insira o mesmo nome de usuário inserido na Etapa 5 para o banco de dados **Conta de Administrador**, insira a senha e clique em **OK**.  
  
         **OR**  
  
    -   Insira outro nome de usuário, insira a senha e clique em OK.  
  
         Você não precisa usar a mesma conta ao criar o banco de dados e o aplicativo Web.  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     Para obter mais informações sobre a caixa de diálogo **Criar Aplicativo Web**, consulte [Caixa de diálogo Criar Aplicativo Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  

    > [!NOTE] 
    >  Se o seu domínio implementar a [Associação de canal ldap 2020 e os requisitos de assinatura LDAP para o Windows](https://support.microsoft.com/en-us/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). Você verá o problema "as credenciais não puderam ser verificadas no Active Directory". Quando você usa a conta de domínio para criar o pool de aplicativos. Para solução alternativa, em vez de usuário de domínio, use um **usuário do computador local**. Isso pode ignorar a verificação de credenciais com Active Directory. Depois de criar o aplicativo Web, você pode alterar a identidade para o usuário do domínio no **Gerenciador do serviços de informações da Internet (IIS)**.
  
12. Na página **Configuração da Web** da caixa **Aplicativo Web** , clique no aplicativo criado e em **Selecionar** na seção  **Associar Aplicativo ao Banco de Dados** .  
  
13. Clique em **Conectar**, selecione o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que você deseja associar ao aplicativo Web e clique em **OK**.  
  
     Você terminou de configurar o site. A página **Configuração da Web** agora exibe o site selecionado, o aplicativo Web criado e o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] associado ao aplicativo.  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. Clique em **Aplicar**. A caixa de mensagem **Configuração Concluída** é exibida. Clique em **OK** na caixa de mensagem para iniciar o aplicativo Web. O endereço do site é https://*nome do servidor* / *Web Application*/. 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
Para obter mais informações sobre as configurações da página Configuração da Web, consulte [Página Configuração da Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 Você também pode usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar configurações para os aplicativos Web e serviços Web associados ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Por exemplo, você pode especificar a frequência com que os dados são carregados ou os emails de validação são enviados. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="deploying-sample-models-and-data"></a><a name="deploySample"></a> Implantar dados e modelos de exemplo  
 Os três pacotes de modelo de exemplo a seguir estão incluídos no  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].   Esses modelos de exemplo incluem dados. **O local padrão dos pacotes de modelo de exemplo é %programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages.**
  
-   chartofaccounts_en.pkg  
-   customer_en.pkg  
-   product_en.pkg  
  
 Você implanta os pacotes usando a ferramenta MDSModelDeploy. O local padrão da ferramenta MDSModelDeploy é *drive*\Arquivos de Programas\Microsoft SQL Server\ 140\Master Data Services\Configuration.  
  
 Para obter informações sobre os pré-requisitos para executar essa ferramenta, consulte [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Para obter informações sobre as atualizações feitas nos dados para dar suporte aos novos recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Exemplos de SQL Server: Pacotes de implantação de modelo (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md).  
  
 **Para implantar modelos de exemplo**  
  
1.  Copie os pacotes de modelo de exemplo em *drive*\Arquivos de Programas\Microsoft SQL Server\140\Master Data Services\Configuration.  
  
2.  Abra um Prompt de Comando Administrador: e procure MDSModelDeploy.exe, executando o comando a seguir.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
    ```  
  
3.  Implante cada um dos modelos de exemplo no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] executando cada um dos comandos a seguir.  
  
    > [!IMPORTANT]  
    >  Nos exemplos abaixo, o valor do serviço do `MDS1` é especificado. Use esse valor se você selecionou  **Site Padrão** ao configurar o site do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Consulte a seção [Configurando o banco de dados e o site](#SetUpWeb) .  
    >   
    >  Se você criou um novo site ou selecionou outro site existente, execute o comando a seguir primeiro para determinar o valor do serviço correto.  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  O primeiro valor do serviço na lista de valores retornados é aquele que você especificou para implantar um modelo.  

    > [!NOTE]
    > Para saber mais sobre as informações de metadados dos modelos de exemplo, consulte o arquivo Leiame disponível neste local "c:\Arquivos de Programas\Microsoft SQL Server\140\Master Data Services\Configuration"
   
     **Para implantar o modelo de exemplo chartofaccounts_en.pkg**  
  
    ```console
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **Para implantar o modelo de exemplo customer_en.pkg**  
  
    ```console
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **Para implantar o modelo de exemplo product_en.pkg**  
  
    ```console
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
    ```  
  
     Quando um modelo é implantado com êxito, a mensagem **operação do MDSModelDeploy concluída** é exibida.  
  
     A imagem a seguir mostra o comando para implantar o modelo de exemplo product_en.pkg.  
  
     ![Linha de comando para implantar o modelo de exemplo de produto](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "Linha de comando para implantar o modelo de exemplo de produto")  
  
4.  Para exibir os modelos de exemplo, faça o seguinte.  
  
    1.  Navegue até o site do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que você configurou. Consulte a seção [Configurando o banco de dados e o site](#SetUpWeb) .  
  
         O endereço do site é https://*nome do servidor* / *Web Application*/.  
  
    2.  Selecione um modelo na caixa de listagem **Modelo** e clique em **Explorer**.  
  
         ![Site da MDS, home page.](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "Site da MDS, home page.")  
  
## <a name="next-step"></a>Próxima etapa  
 Crie um novo modelo e entidades para os dados. Consulte [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) e [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 Para obter uma visão geral de como você pode usar um modelo e entidades para criar uma estrutura para seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Visão geral do MDS &#40;Master Data Services &#41;](../master-data-services/master-data-services-overview-mds.md)  
    
## <a name="see-also"></a>Consulte Também  
 [Banco de dados Master Data Services](../master-data-services/master-data-services-database.md)   
 [Master Data Manager aplicativo Web](../master-data-services/master-data-manager-web-application.md)   
 [Página de configuração do banco de dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Novidades no MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
