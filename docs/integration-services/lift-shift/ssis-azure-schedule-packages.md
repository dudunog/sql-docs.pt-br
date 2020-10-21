---
title: Agendar pacote SSIS no Azure | Microsoft Docs
description: Fornece uma visão geral dos métodos disponíveis para agendar a execução de pacotes SSIS implantados para o Banco de Dados SQL do Azure.
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 7c61b1b032ef4ff08301c91f080f188d89e2aadc
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195168"
---
# <a name="schedule-the-execution-of-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>Agendar a execução de pacotes SSIS (SQL Server Integration Services) implantados no Azure

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



É possível agendar a execução dos pacotes do SSIS implantados no Catálogo do SSISDB em um servidor de Banco de Dados SQL do Azure escolhendo um dos métodos descritos neste artigo. É possível agendar um pacote direta ou indiretamente como parte de um pipeline do Azure Data Factory. Para obter uma visão geral sobre o SSIS no Azure, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](ssis-azure-lift-shift-ssis-packages-overview.md).

- Agendar um pacote indiretamente

  - [Agende com a opção Agendar no SSMS (SQL Server Management Studio)](#ssms)

  - [Trabalhos Elásticos de Banco de Dados SQL](#elastic)

  - [SQL Server Agent](#agent)

- [Agendar um pacote indiretamente como parte de um pipeline do Azure Data Factory](#activity)


## <a name="schedule-a-package-with-ssms"></a><a name="ssms"></a> Agendar um pacote com o SSMS

No SSMS (SQL Server Management Studio), é possível clicar com o botão direito do mouse em um pacote implantado no banco de dados do Catálogo do SSIS, SSISDB, e selecionar **Agendar** para abrir a caixa de diálogo **Nova agenda**. Para obter mais informações, consulte [Agendar pacotes SSIS no Azure com o SSMS](ssis-azure-schedule-packages-ssms.md).

Esse recurso exige o SQL Server Management Studio versão 17.7 ou superior. Para obter a versão mais recente do SSMS, confira [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).

## <a name="schedule-a-package-with-sql-database-elastic-jobs"></a><a name="elastic"></a> Agendar um pacote com trabalhos elásticos de Banco de Dados SQL

Para obter mais informações sobre trabalhos elásticos no Banco de Dados SQL, consulte [Gerenciando bancos de dados de nuvem expandidos](/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Prerequisites

Antes que você possa usar trabalhos elásticos para agendar pacotes do SSIS armazenados no banco de dados de catálogo do SSISDB em um servidor de Banco de Dados SQL do Azure, você deverá fazer o seguinte:

1.  Instale e configure os componentes de trabalhos de banco de dados elástico. Para obter mais informações, consulte [Visão geral da instalação de trabalhos de Banco de Dados Elástico](/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Crie credenciais no escopo do banco de dados que os trabalhos possam usar para enviar comandos para o banco de dados de catálogo do SSIS. Para obter mais informações, veja [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Criar um trabalho elástico

Crie o trabalho usando um script Transact-SQL semelhante ao mostrado no exemplo a seguir:

```sql
-- Create Elastic Jobs target group
EXEC jobs.sp_add_target_group 'TargetGroup'

-- Add Elastic Jobs target group member
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup',
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="schedule-a-package-with-sql-server-agent-on-premises"></a><a name="agent"></a> Agendar um pacote com o SQL Server Agent local

Para obter mais informações sobre o SQL Server Agent, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

### <a name="prerequisite---create-a-linked-server"></a>Pré-requisito – criar um servidor vinculado

Antes de usar o SQL Server Agent local para agendar a execução de pacotes armazenados em um servidor de Banco de Dados SQL do Azure, você precisa adicionar o servidor de Banco de Dados SQL ao seu SQL Server local como um servidor vinculado.

1.  **Configurar o servidor vinculado**

    ```sql
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',     
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location='',
        @provstr='',
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **Configurar as credenciais do servidor vinculado**

    ```sql
    -- Add your Azure SQL Database server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer',
        @useself = 'false',
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **Configurar as opções do servidor vinculado**

    ```sql
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

Para obter mais informações, consulte [Criar servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) e [Servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Criar um trabalho do SQL Server Agent

Para agendar um pacote com o SQL Server Agent local, crie um trabalho com uma etapa de trabalho que chama os procedimentos armazenados do catálogo SSIS `[catalog].[create_execution]` e depois `[catalog].[start_execution]`. Para obter mais informações, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

1.  No SQL Server Management Studio, conecte-se ao banco de dados do SQL Server local no qual você deseja criar o trabalho.

2.  Clique com o botão direito do mouse no nó **SQL Server Agent**, selecione **Novo** e, em seguida, selecione **Trabalho** para abrir a caixa de diálogo **Novo Trabalho**.

3.  Na caixa de diálogo **Novo Trabalho**, selecione a página **Etapas** e, em seguida, selecione **Novo** para abrir a caixa de diálogo **Nova Etapa do Trabalho**.

4.  Na caixa de diálogo **Nova Etapa do Trabalho**, selecione `SSISDB` como o **Banco de dados**.

5.  No campo **Comando**, insira um script do Transact-SQL semelhante ao mostrado no exemplo a seguir:

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
        @folder_name=N'folderName', @project_name=N'projectName', 
        @package_name=N'packageName', @use32bitruntime=0, @runincluster=1, @useanyworker=1,
        @execution_id=@exe_id OUTPUT 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id
    ```

6.  Conclua a configuração e o agendamento do trabalho.

## <a name="schedule-a-package-as-part-of-an-azure-data-factory-pipeline"></a><a name="activity"></a> Agendar um pacote como parte de um pipeline do Azure Data Factory

É possível agendar um pacote indiretamente usando um gatilho para executar um pipeline do Azure Data Factory que executa um pacote do SSIS.

Para agendar um pipeline do Data Factory, use um dos seguintes gatilhos:

- [Gatilho de agendamento](/azure/data-factory/how-to-create-schedule-trigger)

- [Gatilho de janela em cascata](/azure/data-factory/how-to-create-tumbling-window-trigger)

- [Gatilho baseado em evento](/azure/data-factory/how-to-create-event-trigger)

Para executar um pacote do SSIS como parte de um pipeline do Data Factory, use uma das seguintes atividades:

- [Atividade Executar pacote do SSIS](/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).

- [Atividade Procedimento armazenado](/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity).

## <a name="next-steps"></a>Próximas etapas

Revise as opções para executar pacotes do SSIS implantados no Azure. Para obter mais informações, consulte [Executar pacotes SSIS no Azure](ssis-azure-run-packages.md).