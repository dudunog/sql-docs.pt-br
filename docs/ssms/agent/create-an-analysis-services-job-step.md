---
description: Create an Analysis Services Job Step
title: Create an Analysis Services Job Step
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.asquery.execgeneral.f1
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: e65aa07cff708a7112b7a0c4e0bbc0338cb40860
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477107"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Instância Gerenciada de SQL do Azure no SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter mais detalhes.

Este tópico descreve como criar e definir etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que executem comandos e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar etapas de trabalho do SQL Server usando comandos e/ou consultas do Analysis Services com:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   Se a etapa de trabalho usar um comando do Analysis Services, a instrução de comando deverá ser o método **Execute** do XML for Analysis Services. A instrução não pode conter um envelope do protocolo SOAP completo nem o método **Discover** do XML for Analysis. Embora o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofereça suporte a envelopes SOAP completos e ao método **Discover** , as etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não oferecem. Para obter mais informações sobre o XML for Analysis Services, consulte [Visão geral do XMLA (XML for Analysis)](/previous-versions/sql/).  
  
-   Se a etapa de trabalho usar uma consulta do Analysis Services, a instrução de consulta deverá ser uma consulta MDX. Para obter mais informações sobre o MDX, consulte [Conceitos básicos da instrução MDX](/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services?viewFallbackFrom=sql-server-ver15).  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
  
-   Para executar uma etapa de trabalho que use o subsistema Analysis Services, o usuário deve ser um membro da função de servidor fixa **sysadmin** ou ter acesso a uma conta proxy válida definida para usar esse subsistema. Além disso, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou o proxy deve ser um administrador do Analysis Services e uma conta de domínio do Windows válida.  
  
-   Apenas membros da função de servidor fixa **sysadmin** podem gravar em arquivo a saída de uma etapa de trabalho. Se a etapa de trabalho for executada por usuários membros da função de banco de dados **SQLAgentUserRole** no banco de dados **msdb** , a saída poderá ser gravada apenas em uma tabela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent grava a saída da etapa de trabalho na tabela **sysjobstepslog** do banco de dados **msdb** .  
  
-   Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para criar uma etapa de trabalho de comando do Analysis Services  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criar trabalhos](../../ssms/agent/create-jobs.md).  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite um trabalho **Step name**(Nome da etapa).  
  
5.  Na lista **Tipo** , clique em **Comando do SQL Server Analysis Services**.  
  
6.  Na lista **Executar como** , selecione um proxy que tenha sido definido para usar o subsistema Comando do Analysis Services. Um usuário membro da função de servidor fixa **sysadmin** também pode selecionar **Conta de Serviço do SQL Agent** para executar essa etapa de trabalho.  
  
7.  Selecione o **Servidor** onde a etapa de trabalho será executada ou digite o nome do servidor.  
  
8.  Na caixa **Comando** , digite a instrução a executar ou clique em **Abrir** para selecionar uma instrução.  
  
9. Clique na página **Avançado** para definir opções para essa etapa de trabalho, como a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tomar em caso de êxito ou falha da etapa, quantas vezes a etapa deve ser tentada e onde deve ser gravada sua saída.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para criar uma etapa de trabalho de consulta do Analysis Services  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criar trabalhos](../../ssms/agent/create-jobs.md).  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa** de trabalho.  
  
5.  Na lista **Tipo** , clique em **Consulta do SQL Server Analysis Services**.  
  
6.  Na lista **Executar como** , selecione um proxy que tenha sido definido para usar o subsistema Consulta do Analysis Services. Um usuário membro da função de servidor fixa **sysadmin** também pode selecionar **Conta de Serviço do SQL Agent** para executar essa etapa de trabalho.  
  
7.  Selecione o **Servidor** e o **Banco de Dados** onde a etapa de trabalho será executada ou digite o nome do servidor ou do banco de dados.  
  
8.  Na caixa **Comando** , digite a instrução a executar ou clique em **Abrir** para selecionar uma instrução.  
  
9. Clique na página **Avançado** para definir opções para essa etapa de trabalho, como a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tomar em caso de êxito ou falha da etapa, quantas vezes a etapa deve ser tentada e onde deve ser gravada sua saída.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para criar uma etapa de trabalho de comando do Analysis Services  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md).  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para criar uma etapa de trabalho de consulta do Analysis Services  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md).  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando o SQL Server Management Objects  
**Para criar uma etapa de trabalho de script PowerShell**  
  
Use a classe **JobStep** com uma linguagem de programação à sua escolha, como XMLA ou MDX. Para obter mais informações, veja [SMO (SQL Server Management Objects)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md).  
