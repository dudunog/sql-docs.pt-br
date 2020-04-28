---
title: Instalar o SQL Server 2014 no Server Core | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3e244b2c4892d725e8e3ddf684b55a224138a50
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637679"
---
# <a name="install-sql-server-2014-on-server-core"></a>Instalar o SQL Server 2014 no Server Core
  Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 ou do [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Este tópico apresenta detalhes de configuração específicos sobre a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core.  
  
 A opção de instalação do Server Core para o sistema operacional [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] oferece um ambiente mínimo para a execução de funções de servidor específicas. Isso ajuda a reduzir os requisitos de manutenção e gerenciamento e a superfície de ataque para essas funções de servidor. Para obter mais informações sobre o Server Core conforme [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]implementado em, consulte [Server Core para Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=202439) (https://go.microsoft.com/fwlink/?LinkId=202439). Para obter mais informações sobre o Server Core conforme [!INCLUDE[win8srv](../../includes/win8srv-md.md)]implementado em, consulte [Server Core for Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx).  
  
## <a name="prerequisites"></a>Prerequisites  
  
|Requisito|Como instalar o|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|Incluído na instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Se essa opção não estiver habilitada, ela será habilitada por padrão pela Instalação.<br /><br /> Não é possível executar as versões 2.0, 3.0 e 3.5 lado a lado em um computador. Ao instalar o .NET Framework 3.5 SP1, você obtém as camadas de 2.0 e 3.0 automaticamente.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|Incluído na instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. Se essa opção não estiver habilitada, ela será habilitada por padrão pela Instalação.<br /><br /> Em um computador com o sistema operacional Windows, você deverá baixar e instalar o .NET Framework 3.5 SP1 antes de executar a Instalação, para instalar os componentes dependentes do .NET 3.5 SP1.<br /><br /> Para obter mais informações sobre as recomendações e diretrizes sobre como adquirir e habilitar o .NET Framework 3,5 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]no, consulte [considerações de implantação do Microsoft .NET Framework 3,5](https://msdn.microsoft.com/library/windows/hardware/hh975396) (https://msdn.microsoft.com/library/windows/hardware/hh975396).|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|Para todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , exceto [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a Instalação instala o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile como pré-requisito.<br /><br /> Para [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]o, baixe [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] o perfil do 4 Server Core do [Microsoft .NET Framework 4 (instalador autônomo) para o Server Core](https://www.microsoft.com/download/details.aspx?id=17718) (https://www.microsoft.com/download/details.aspx?id=17718)e instale-o antes de prosseguir com a instalação.|  
|Windows Installer 4.5|Enviado com a instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|Windows PowerShell 2.0|Enviado com a instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
  
##  <a name="supported-features"></a><a name="BK_SupportedFeatures"></a> Recursos com suporte  
 Use a tabela a seguir para descobrir quais recursos têm suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|Recurso|Com suporte|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Serviços|Sim|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replicação|Sim|  
|Pesquisa de Texto Completo|Sim|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Sim|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Não|  
|SSDT ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools)|Não|  
|Conectividade das ferramentas de cliente|Sim|  
|Servidor Integration Services<sup>[1]</sup>|Sim|  
|Compatibilidade das ferramentas de cliente com versões anteriores|Não|  
|SDK de Ferramentas de cliente|Não|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online|Não|  
|Ferramentas de Gerenciamento - Básicas|Somente remoto<sup>[2]</sup>|  
|Ferramentas de Gerenciamento – Completas|Somente remoto<sup>[2]</sup>|  
|Distributed Replay Controller|Não|  
|Distributed Replay Client|Somente remoto<sup>[2]</sup>|  
|SDK de Conectividade de Cliente do SQL|Sim|  
|Microsoft Sync Framework|Sim<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Não|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|Não|  
  
 <sup>[1]</sup> Para obter mais informações sobre o novo Integration Services Server e seus recursos [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no, consulte [Integration Services &#40;SSIS&#41; Server](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md).  
  
 <sup>[2]</sup> Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente, que não seja o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, e conectados aos serviços de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.  
  
 <sup>[3]</sup> O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Microsoft Sync Framework não está incluído no pacote de instalação. Você pode baixar a versão apropriada do Sync Framework deste [centro de download](https://go.microsoft.com/fwlink/?LinkId=221788) da Microsofthttps://go.microsoft.com/fwlink/?LinkId=221788) (página e instalá-la em um computador que esteja executando a instalação [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] do Server [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Core do SP1 ou.  
  
## <a name="supported-scenario-matrix"></a>Matriz de cenários com suporte  
 A tabela a seguir mostra a matriz de cenários com suporte para a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|||  
|-|-|  
|Edições do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] as edições de 64 bits<sup>[1]</sup>|  
|Idioma do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todos os idiomas|  
|Idioma do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na combinação de idioma/localidade do sistema operacional|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em japonês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em alemão<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em chinês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em árabe<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em tailandês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em turco<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em português (Portugal)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em inglês|  
|Windows Edition|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bits x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bits x64 Standard<br /><br /> Server Core do[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bits x64 Data Center<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core do SP1 64 bits x64 Enterprise<br /><br /> Server Core do[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bits x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core do SP1 64 bits x64 Web|  
  
 <sup>[1]</sup> Não há suporte para a instalação da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão de 32 bits das edições no Server Core.  
  
## <a name="upgrading"></a>Atualizando  
 Em instalações do Server Core, atualizar de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tem suporte.  
  
## <a name="installation"></a>Instalação  
 O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não tem suporte para a instalação por meio do assistente de instalação no sistema operacional Server Core. Quando você faz a instalação no Server Core, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. Para obter mais informações, consulte [Install SQL Server 2014 from the Command Prompt](install-sql-server-from-the-command-prompt.md) (Instalar o SQL Server 2014 do Prompt de Comando).  
  
> [!IMPORTANT]  
>  Não é possível instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core.  
  
 Independentemente do método de instalação, é necessário confirmar a aceitação dos termos da licença de software como indivíduo ou em nome de uma entidade, a menos que o uso do software seja governado por um contrato separado, como um contrato de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um contrato de terceiros com um ISV ou OEM.  
  
 Os termos da licença são exibidos para exame e aceitação na interface do usuário da Instalação. As instalações autônomas (usando o parâmetro /Q ou /QS) devem incluir o parâmetro /IACCEPTSQLSERVERLICENSETERMS. Você pode analisar as condições de licença separadamente em [Microsoft Software License Terms](https://go.microsoft.com/fwlink/?LinkId=148209)(em inglês).  
  
> [!NOTE]  
>  Dependendo de como você recebeu o software (por exemplo, por meio de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), o uso do software pode estar sujeito a termos e condições adicionais.  
  
 Para instalar recursos específicos, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos. Para obter mais informações sobre os parâmetros de recursos e seu uso, consulte as seções a seguir.  
  
### <a name="feature-parameters"></a>Parâmetros de recursos  
  
|Parâmetro de recurso|DESCRIÇÃO|  
|-----------------------|-----------------|  
|SQLENGINE|Instala apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|REPLICAÇÃO|Instala o componente Replicação juntamente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|FULLTEXT|Instala o componente FullText com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|AS|Instala todos os componentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|IS|Instala todos os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|CONN|Instala os componentes de conectividade.|  
  
 Veja os exemplos a seguir do uso de parâmetros de recurso:  
  
|Parâmetro e valores|Descrição|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Instala apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|/FEATURES=SQLEngine,FullText|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o texto completo.|  
|/FEATURES=SQLEngine,Conn|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os componentes de conectividade.|  
|/FEATURES=SQLEngine,AS,IS,Conn|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e os componentes de conectividade.|  
  
### <a name="installation-options"></a>Opções de instalação  
 A Instalação dá suporte às opções de instalação a seguir enquanto instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um sistema operacional do Server Core:  
  
1.  **Instalação da linha de comando**  
  
     Para instalar recursos específicos usando a opção de instalação do prompt de comando, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos listados. Um exemplo de como usar os parâmetros a partir da linha de comando é apresentado a seguir:  
  
    ```cmd
    setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Instalação usando o arquivo de configuração**  
  
     A Instalação dá suporte ao uso do arquivo de configuração apenas através do prompt de comando. O arquivo de configuração é um arquivo de texto com a estrutura básica de um parâmetro (par de nome/valor) e um comentário descritivo. O arquivo de configuração especificado no prompt de comando deve ter uma extensão de nome de arquivo .INI. Veja a seguir exemplos de ConfigurationFile.INI:  
  
    -   Instalando o [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
         O exemplo a seguir mostra como instalar uma nova instância autônoma que inclui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"
        ```  
  
    -   Instalando componentes de conectividade  
  
         O exemplo a seguir mostra como instalar os componentes de conectividade:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True
        ```  
  
    -   Instalando todos os recursos com suporte  
  
         O exemplo a seguir mostra como instalar todos os recursos com suporte do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     Os exemplos a seguir mostram como você pode iniciar a Instalação usando um arquivo de configuração.  
  
    -   Arquivo de configuração  
  
         Os exemplos a seguir mostram como usar o arquivo de configuração:  
  
        -   Para especificar o arquivo de configuração no prompt de comando:  
  
        ```cmd
        setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   Para especificar senhas no prompt de comando em vez de no arquivo de configuração:  
  
        ```cmd
        setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         Se o arquivo DefaultSetup.ini estiver nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra o arquivo DefaultSetup.ini e adicione o parâmetro *Features* a ele.  
  
         Se o arquivo DefaultSetup.ini não existir, você poderá criá-lo e copiá-lo nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="configuring-remote-access-of-ssnoversion-running-on-server-core"></a>Configurando o acesso remoto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core  
 Execute as ações descritas abaixo para configurar o acesso remoto de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em execução em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
### <a name="enable-remote-connections-on-the-instance-of-ssnoversion"></a>Habilitar conexões remotas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Para habilitar conexões remotas, use o SQLCMD.exe localmente e execute as instruções a seguir na instância do Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-ssnoversion-browser-service"></a>Habilitar e iniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 Por padrão, o serviço Navegador está desabilitado.  Se ele estiver desabilitado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core, execute o seguinte comando no prompt de comando para habilitá-lo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Depois de habilitá-lo, execute o seguinte comando a partir do prompt de comando para iniciar o serviço:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Criar exceções no Firewall do Windows  
 Para criar exceções para o acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Firewall do Windows, siga as etapas especificadas em [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-ssnoversion"></a>Habilitar TCP/IP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O protocolo TCP/IP pode ser habilitado por meio do Windows PowerShell para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core. Siga estas etapas:  
  
1.  No computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, inicie o Gerenciador de Tarefas.  
  
2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
  
3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **sqlps.exe** no campo **Abrir** e clique em **OK**. Isso abre a janela do ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** .  
  
4.  Na janela **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**, execute o script a seguir para habilitar o protocolo TCP/IP:  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = New-Object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>Desinstalação  
 Depois que fizer logon em um computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, você terá um ambiente de desktop limitado com um prompt de comando de Administrador. Você pode usar esse prompt de comando para iniciar a desinstalação de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para desinstalar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inicie a desinstalação do prompt de comando no modo silencioso completo usando o parâmetro /Q ou no modo silencioso simples usando o parâmetro /QS. O parâmetro /QS mostra o progresso por meio da interface de usuário, mas não aceita nenhuma entrada. /Q é executado no modo silencioso sem nenhuma interface de usuário.  
  
 Para desinstalar uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```cmd
setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Para remover uma instância nomeada, especifique o nome da instância, em vez de "MSSQLSERVER" no exemplo anterior.  
  
> [!WARNING]
>  Se você fechar acidentalmente o prompt de comando, siga estas etapas para iniciar um novo prompt de comando:  
> 
>  1.  Pressione Ctrl+Shift+Esc para exibir o Gerenciador de Tarefas.  
> 2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
> 3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **cmd** no campo **Abrir** e [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2014 usando um arquivo de configuração](install-sql-server-using-a-configuration-file.md)   
 [Instalar o SQL Server 2014 no prompt de comando](install-sql-server-from-the-command-prompt.md)   
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Guia de Introdução da opção de instalação do Server Core](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [Configurando uma instalação do Server Core: visão geral](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Cmdlets de cluster de failover no Windows PowerShell listados por foco de tarefa](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [Mapeamento de comandos do Cluster.exe para cmdlets do Windows PowerShell para clusters de failover](https://go.microsoft.com/fwlink/?LinkId=221421)  
