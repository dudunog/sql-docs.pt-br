---
title: Remover o envio de logs secundário
description: Saiba como remover um parceiro secundário de envio de logs usando o SQL Server Management Studio ou o Transact-SQL no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: db79ab9084e1c633af66736d6974487e00182385
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85695752"
---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>Remova um banco de dados secundário de uma configuração de envio de logs (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como remover um banco de dados secundário de envio de logs no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para remover um banco de dados secundário de envio de logs, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>Para remover um banco de dados secundário de envio de logs  
  
1.  Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é no momento o servidor primário para envio de logs e expanda essa instância.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados primário de envio de logs e clique em **Propriedades**.  
  
3.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
4.  Em **Instâncias e banco de dados do servidor secundário**, clique no banco de dados que você deseja remover.  
  
5.  Clique em **Remover**.  
  
6.  Clique em **OK** para atualizar a configuração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-remove-a-secondary-database"></a>Para remover um banco de dados secundário  
  
1.  No servidor primário, execute [sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md) para excluir as informações sobre o banco de dados secundário do servidor primário.  
  
2.  No servidor secundário, execute [sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md) para excluir o banco de dados secundário.  
  
    > [!NOTE]  
    >  Se não houver outro banco de dados secundário com a mesma ID secundária, **sp_delete_log_shipping_secondary_primary** será invocado de **sp_delete_log_shipping_secondary_database** e excluirá a entrada da ID secundária e os trabalhos de cópia e restauração.  
  
3.  No servidor secundário, desabilite os trabalhos de cópia e restauração. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Adicionar um banco de dados secundário a uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
