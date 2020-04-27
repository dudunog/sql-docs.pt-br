---
title: Adicionar um banco de dados secundário a uma configuração de envio de logs (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- adding secondary databases
- secondary databases [SQL Server], in log shipping
- secondary data files [SQL Server], adding
- log shipping [SQL Server], secondary databases
ms.assetid: b02eba13-f8e6-4684-b7e4-75ea038ea473
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22f1fbc9470eb4002bb40f0e4e513f35134c442e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774329"
---
# <a name="add-a-secondary-database-to-a-log-shipping-configuration-sql-server"></a>Adicionar um banco de dados secundário a uma configuração de envio de logs (SQL Server)
  Este tópico descreve como adicionar um banco de dados secundário a uma configuração de envio de logs existente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para adicionar um banco de dados secundário de envio de logs, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>Para adicionar um banco de dados secundário de envio de logs  
  
1.  Clique com o botão direito do mouse no banco de dados que deve ser usado como banco de dados primário na configuração de envio de logs e clique em **Propriedades**.  
  
2.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
3.  Em **Instâncias e bancos de dados do servidor secundário**, clique em **Adicionar**.  
  
4.  Clique em **Conectar** e conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar como servidor secundário.  
  
5.  Na caixa **banco de dados secundário** , escolha um banco de dados na lista ou digite o nome do banco de dados que você deseja criar.  
  
6.  Na guia **Inicializar banco de dados secundário** , escolha a opção que deseja usar para inicializar o banco de dados secundário.  
  
7.  Na **Guia Copiar Arquivos**, na caixa **Pasta de destino para arquivos copiados** , digite o caminho da pasta para a qual os backups de log de transações devem ser copiados. Essa pasta fica, frequentemente, alocada no servidor secundário.  
  
8.  Observe a agenda de cópias listada na caixa **Agenda** em **Copiar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
9. Na guia **Restaurar** em **Estado de banco de dados ao restaurar backups**, escolha a opção **Nenhum modo de recuperação** ou **Modo de espera** .  
  
10. Caso tenha escolhido a opção **Modo de espera** , escolha se deseja desconectar os usuários do banco de dados secundário enquanto a operação de restauração está em andamento.  
  
11. Caso queira adiar o processo de restauração no servidor secundário, escolha um tempo de atraso em **Atrasar restauração de backups pelo menos**.  
  
12. Escolha um limite de alerta em **Alertar se nenhuma restauração ocorrer em**.  
  
13. Observe a agenda de restauração listada na caixa **Agenda** em **Restaurar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
14. Clique em **OK**.  
  
15. Clique em **OK** na caixa de diálogo Propriedades do Banco de Dados para iniciar o processo de configuração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>Para adicionar um banco de dados secundário de envio de logs  
  
1.  No servidor secundário, execute [sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql) fornecendo os detalhes do servidor primário e banco de dados. Esse procedimento armazenado retorna a ID secundária e as ID de tarefa de cópia e restauração.  
  
2.  No servidor secundário, execute [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) para definir o agendamento das tarefas de cópia e restauração.  
  
3.  No servidor secundário, execute [sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql) para adicionar o banco de dados secundário.  
  
4.  No servidor primário, execute [sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql) para adicionar as informações necessárias sobre o novo banco de dados secundário ao servidor primário.  
  
5.  No servidor secundário, habilite as tarefas de cópia e restauração. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizar o envio de logs para SQL Server 2014 &#40;Transact-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [Remover um banco de dados secundário de uma configuração de envio de logs &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Log Shipping Tables and Stored Procedures](log-shipping-tables-and-stored-procedures.md)  
  
  
