---
description: Crie um trabalho
title: Crie um trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 404971a6874de15cfae2408e5fa2d4bc2e387c0e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039170"
---
# <a name="create-a-job"></a>Crie um trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como criar um trabalho do SQL Server Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SMO (SQL Server Management Objects).  
  
Para adicionar etapas de trabalho, agendas, alertas e notificações que podem ser enviadas a operadores, consulte os tópicos na seção Consulte também.  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar um trabalho, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure),  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SQL Server Management Objects](#SMOProcedure)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
-   Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
-   Trabalhos locais são armazenados em cache pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent local. Portanto, qualquer modificação obriga, implicitamente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a rearmazenar em cache o trabalho. Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não armazena o trabalho em cache até que **sp_add_jobserver** seja chamado, é mais eficiente chamar **sp_add_jobserver** por último.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
-   Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
-   Por questão de segurança, apenas o proprietário do trabalho ou um membro da função **sysadmin** pode alterar a definição do trabalho. Somente os membros da função de servidor fixa **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário.  
  
    > [!NOTE]  
    > Se você transmitir a propriedade a um usuário que não seja membro da função de servidor fixa **sysadmin** e o trabalho estiver executando etapas que exijam contas proxy (por exemplo, execução de pacotes [!INCLUDE[ssIS](../../includes/ssis_md.md)] ), verifique se o usuário tem acesso à conta proxy necessária, ou o trabalho falhará.  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para criar um trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar o trabalho do SQL Server Agent.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Novo Trabalho...**.  
  
4.  Na caixa de diálogo **Novo Trabalho** , na página **Geral** , modifique as propriedades gerais do trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Geral&#41;](../../ssms/agent/job-properties-new-job-general-page.md)  
  
5.  Na página **Etapas** , organize as etapas de trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Etapas&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)  
  
6.  Na página **Agendas** , organize agendas para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Agendamentos&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)  
  
7.  Na página **Alertas** , organize os alertas para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Alertas&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)  
  
8.  Na página **Notificações**, defina ações para que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seja executado quando o trabalho for concluído. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Notificações&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md).  
  
9. Na página **Destinos** , gerencie os servidores de destino para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Destinos&#41;](../../ssms/agent/job-properties-new-job-targets-page.md).  
  
10. Quando terminar, clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para criar um trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
Para obter mais informações, consulte:  
  
-   [sp_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)  
  
-   [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_add_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
-   [sp_attach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_add_jobserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)  
  
## <a name="using-sql-server-management-objects"></a><a name="SMOProcedure"></a>Usando o SQL Server Management Objects  
**Para criar um trabalho do SQL Server Agent**  
  
Chame o método **Create** da classe **Job** usando uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md).  
