---
title: Criar um trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: stevestein
ms.author: sstein
ms.openlocfilehash: de74f032924fbb0b6643bd8f3d482481ffb1f983
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067822"
---
# <a name="create-a-job"></a>Crie um trabalho
  Este tópico descreve como criar um trabalho do SQL Server Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SMO (SQL Server Management Objects).  
  
 Para adicionar etapas de trabalho, agendas, alertas e notificações que podem ser enviadas a operadores, consulte os tópicos na seção Consulte também.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um trabalho, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure),  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server Management Objects](#SMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
-   Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
-   Trabalhos locais são armazenados em cache pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent local. Portanto, qualquer modificação obriga, implicitamente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a rearmazenar em cache o trabalho. Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não armazena o trabalho em cache até que **sp_add_jobserver** seja chamado, é mais eficiente chamar **sp_add_jobserver** por último.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
-   Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
-   Por questão de segurança, apenas o proprietário do trabalho ou um membro da função **sysadmin** pode alterar a definição do trabalho. Somente os membros da função de servidor fixa **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário.  
  
    > [!NOTE]  
    >  Se você transmitir a propriedade a um usuário que não seja membro da função de servidor fixa **sysadmin** e o trabalho estiver executando etapas que exijam contas proxy (por exemplo, execução de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] ), verifique se o usuário tem acesso à conta proxy necessária, ou o trabalho falhará.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para criar um trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar o trabalho do SQL Server Agent.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Novo Trabalho...**.  
  
4.  Na caixa de diálogo **Novo Trabalho** , na página **Geral** , modifique as propriedades gerais do trabalho. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho e novo trabalho &#40;página geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  Na página **Etapas** , organize as etapas de trabalho. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho: página de etapas do novo trabalho &#40;&#41;](job-properties-new-job-steps-page.md)  
  
6.  Na página **Agendas** , organize agendas para o trabalho. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho: nova página de agendas de &#40;de trabalho&#41;](job-properties-new-job-schedules-page.md)  
  
7.  Na página **Alertas** , organize os alertas para o trabalho. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho: nova página de alertas de &#40;de trabalho&#41;](job-properties-new-job-alerts-page.md)  
  
8.  Na página **Notificações**, defina ações para que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seja executado quando o trabalho for concluído. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho: nova página de notificações de &#40;de trabalho&#41;](job-properties-new-job-notifications-page.md).  
  
9. Na página **Destinos** , gerencie os servidores de destino para o trabalho. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Propriedades do trabalho: nova página de destinos de &#40;de trabalho&#41;](job-properties-new-job-targets-page.md).  
  
10. Ao concluir, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para criar um trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
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
  
-   [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [&#41;&#40;Transact-SQL de sp_add_jobserver](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMOProcedure"></a>Usando SQL Server Management Objects  
 **Para criar um trabalho do SQL Server Agent**  
  
 Chame o método `Create` da classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](sql-server-agent.md).  
  
##  <a name="SSMSProc2"></a>  
