---
title: Implantar e executar um pacote SSIS no Azure | Microsoft Docs
description: Saiba como implantar um projeto do SSIS (SQL Server Integration Services) no Catálogo do SSIS no Banco de Dados SQL do Azure, executar um pacote
ms.date: 05/22/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 42250d8edbd646f9bd89f3663f2591b3404fe05f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68007945"
---
# <a name="tutorial-deploy-and-run-a-sql-server-integration-services-ssis-package-in-azure"></a>Tutorial: Implantar e executar um pacote SSIS (SQL Server Integration Services) no Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tutorial mostra como implantar um projeto do SSIS (SQL Server Integration Services) no Catálogo do SSIS no Banco de Dados SQL do Azure, executar um pacote no Azure-SSIS Integration Runtime e monitorar o pacote em execução.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você tem a versão 17.2 ou posterior do SQL Server Management Studio. Para baixar a versão mais recente do SSMS, veja [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Verifique também se você configurou o banco de dados do SSISDB no Azure e provisionou o Azure-SSIS Integration Runtime. Para obter informações sobre como provisionar o SSIS no Azure, consulte [Implantar pacotes do SQL Server Integration Services no Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para executar o pacote no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [Portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.

## <a name="connect-to-the-ssisdb-database"></a>Conectar-se ao banco de dados SSISDB

Use o SQL Server Management Studio para se conectar ao catálogo do SSIS no seu servidor de Banco de Dados SQL do Azure. Para saber mais e ver capturas de tela, confira o artigo [Conectar-se ao Banco de dados do catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

Aqui estão as duas coisas mais importantes para lembrar. Essas etapas estão descritas no procedimento a seguir.
-   Insira o nome totalmente qualificado do servidor do Banco de Dados SQL do Azure no formato **mysqldbserver.database.windows.net**.
-   Selecione o `SSISDB` como o banco de dados da conexão.

> [!IMPORTANT]
> Um servidor do Banco de Dados SQL do Azure escuta na porta 1433. Se você estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

1. Abra o SQL Server Management Studio.

2. **Conecte-se ao servidor**. Na caixa de diálogo **Conectar ao Servidor**, insira as informações a seguir:

   | Configuração       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de Banco de Dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve estar neste formato: **mysqldbserver.database.windows.net**. Se você precisar do nome do servidor, consulte [Conectar-se ao banco de dados do Catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md). |
   | **Autenticação** | Autenticação do SQL Server | Você não pode se conectar ao Banco de Dados SQL do Azure com a Autenticação do Windows. |
   | **Logon** | A conta do administrador do servidor | A conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta do administrador do servidor | A senha que você especificou quando criou o servidor. |

3. **Conecte-se ao banco de dados SSISDB**. Selecione **Opções** para expandir a caixa de diálogo **Conectar ao Servidor**. Na caixa de diálogo **conectar ao servidor**, selecione a guia **Propriedades de Conexão**. No campo **Conectar-se ao banco de dados**, selecione ou insira `SSISDB`.

4. Depois, selecione **Conectar**. A janela Pesquisador de Objetos será aberta no SSMS. 

5. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

## <a name="deploy-a-project-with-the-deployment-wizard"></a>Implantar um projeto com o Assistente de Implantação

Para saber mais sobre como implantar pacotes e conhecer o Assistente de Implantação, confira [Implantar pacotes e projetos do SSIS (Integration Services)](../packages/deploy-integration-services-ssis-projects-and-packages.md) e [Assistente de Implantação do Integration Services](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

> [!NOTE]
> A implantação no Azure tem suporte apenas para o Modelo de Implantação de Projeto.

### <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de Implantação do Integration Services
1. No Pesquisador de Objetos no SSMS, com o nó **Catálogos do Integration Services** e o nó **SSISDB** expandidos, expanda a pasta do projeto.

2.  Selecione o nó **Projetos**.

3.  Clique com o botão direito do mouse no nó **Projetos** e selecione **Implantar projeto**. O Assistente de Implantação do Integration Services será aberto. Implante um projeto de um banco de dados de catálogo do SSIS ou do sistema de arquivos.

    ![Implantar um projeto do SSMS](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![A caixa de diálogo do Assistente de Implantação do SSIS é exibida](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Implantar um projeto com o Assistente de Implantação
1. Na página **Introdução** do Assistente de Implantação, examine a introdução. Selecione **Avançar** para abrir a página **Selecionar Origem**.

2. Na página **Selecionar Origem**, selecione o projeto existente do SSIS a ser implantado.
    -   Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac.
    -   Para implantar um projeto que reside em um catálogo do SSIS, selecione **Catálogo do Integration Services** e, em seguida, insira o nome do servidor e o caminho para o projeto no catálogo.
    -   Selecione **Avançar** para ver a página **Selecionar Destino**.
  
3.  Na página **Selecionar Destino**, selecione o destino para o projeto.
    -   Insira o nome do servidor totalmente qualificado no formato `<server_name>.database.windows.net`.
    -   Forneça informações de autenticação e selecione **Conectar**.
    -   Em seguida, selecione **Procurar** para selecionar a pasta de destino no SSISDB.
    -   Selecione **Avançar** para abrir a página **Examinar**. (O botão **Avançar** é habilitado somente depois de selecionar **Conectar**.)
  
4.  Na página **Examinar**, examine as configurações selecionadas.
    -   Você pode alterar suas seleções selecionando **Anterior** ou selecionando qualquer uma das etapas no painel esquerdo.
    -   Selecione **Implantar** para iniciar o processo de implantação.

    > [!NOTE]
    > Se você receber a mensagem de erro **Não há nenhum agente de trabalho ativo. (Provedor de dados do .Net SqlClient)** , verifique se o Azure-SSIS Integration Runtime está em execução. Esse erro ocorre se você tenta implantar enquanto o tempo de execução de integração do Azure-SSIS está em um estado parado.

5.  Após a conclusão do processo de implantação, a página **Resultados** será aberta. Essa página exibe o êxito ou a falha de cada ação.
    -   Se a ação falhou, selecione **Com falha** na coluna **Resultado** para exibir uma explicação do erro.
    -   Opcionalmente, selecione **Salvar Relatório...** para salvar os resultados em um arquivo XML.
    -   Selecione **Fechar** para sair do assistente.

## <a name="deploy-a-project-with-powershell"></a>Implantar um projeto com o PowerShell

Para implantar um projeto com o PowerShell para o SSISDB no Banco de Dados SQL do Azure, adapte o script a seguir aos seus requisitos. O script enumera as pastas filho em `$ProjectFilePath` e os projetos na pasta cada filho. Em seguida, cria as mesmas pastas no SSISDB e implanta os projetos nessas pastas.

Este script requer o SQL Server Data Tools versão 17.x ou o SQL Server Management Studio instalado no computador em que você executa o script.

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>Executar um pacote

1. No Pesquisador de Objetos no SSMS, selecione o pacote que você deseja executar.

2. Clique com o botão direito do mouse e selecione **Executar** para abrir a caixa de diálogo **Executar Pacote**.

3.  Na caixa de diálogo **Executar Pacote**, configure a execução de pacote usando as configurações nas guias **Parâmetros**, **Gerenciadores de Conexões** e **Avançado**.

4.  Selecione **OK** para executar o pacote.

## <a name="monitor-the-running-package-in-ssms"></a>Monitorar o pacote em execução no SSMS

Para exibir o status de operações do Integration Services em execução no momento no servidor do Integration Services, tais como implantação, validação e execução de pacotes, use a caixa de diálogo **Operações Ativas** no SSMS. Para abrir a caixa de diálogo **Operações Ativas**, clique com o botão direito do mouse em **SSISDB** e, em seguida, selecione **Operações Ativas**.

Você também pode selecionar um pacote no Pesquisador de Objetos, clicar com o botão direito do mouse e selecionar, sucessivamente, **Relatórios**, **Relatórios Padrão** e **Todas as Execuções**.

Para obter mais informações sobre como monitorar pacotes em execução no SSMS, consulte [Monitorar pacotes em execução e outras operações](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations).

## <a name="monitor-the-execute-ssis-package-activity"></a>Monitorar a atividade Executar pacote do SSIS

Se estiver executando um pacote como parte de um pipeline do Azure Data Factory com a atividade Executar pacote do SSIS, será possível monitorar as execuções do pipeline na interface do usuário do Data Factory. É possível obter a ID de execução do SSISDB da saída da execução da atividade e usar a ID para verificar mensagens de erro e logs de execução mais abrangentes no SSMS.

![Obter a ID de execução do pacote no Data Factory](media/ssis-azure-deploy-run-monitor-tutorial/get-execution-id.png)

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Monitorar o Azure-SSIS Integration Runtime

Para obter informações de status sobre o Azure-SSIS Integration Runtime em que os pacotes estão em execução, use os comandos do PowerShell a seguir. Para cada um dos comandos, forneça os nomes de Data Factory, o Azure-SSIS IR e o grupo de recursos.

Para obter mais informações, consulte [Monitorar o Azure-SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime).

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Obter metadados sobre o Azure-SSIS Integration Runtime

```powershell
Get-AzDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Obter o status do Azure-SSIS Integration Runtime

```powershell
Get-AzDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Próximas etapas
- Saiba como agendar a execução de pacotes. Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md)
