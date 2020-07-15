---
title: Failover para um envio de logs secundário
description: Saiba como fazer failover para um secundário de envio de logs do SQL Server usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ba01642d09e9352b976978df1cfc78756ad79029
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85696189"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>Failover para um envio de logs secundário (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O failover para um envio de logs secundário será útil se a instância do servidor primário falhar ou requerer manutenção.  
  
## <a name="preparing-for-a-controlled-failover"></a>Preparando para um failover controlado  
 Geralmente, os bancos de dados primário e secundário não são sincronizados porque o banco de dados primário continua sendo atualizado após seu último trabalho de backup. Além disso, em alguns casos, os backups de log de transações recentes não foram copiados nas instâncias do servidor secundário ou alguns backups de log copiados talvez ainda não tenham sido aplicados ao banco de dados secundário. Recomendamos que você comece sincronizando todos os bancos de dados secundários com o banco de dados primário, se possível.  
  
 Para obter informações sobre trabalhos do envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="failing-over"></a>Fazendo failover  
 Para fazer failover para um banco de dados secundário:  
  
1.  Copie qualquer arquivo de backup não copiado do compartilhamento de backup na pasta de destino de cópia de cada servidor secundário.  
  
2.  Aplique qualquer backup de log de transações não aplicado em sequência em cada banco de dados secundário. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
3.  Se o banco de dados primário estiver acessível, faça backup do log de transações ativas e aplique-o aos bancos de dados secundários. Talvez seja necessário definir o banco de dados para o [modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md) para obter acesso exclusivo antes de emitir o comando de restauração e, em seguida, alterá-lo para vários usuários após a conclusão da restauração.  
  
     Se a instância de servidor primário original não estiver danificada, faça backup da parte final do log de transações do banco de dados primário usando WITH NORECOVERY. Isso deixa o banco de dados no estado de restauração e, portanto, indisponível aos usuários. Eventualmente você poderá avançar a rolagem desse banco de dados aplicando backups de log de transações do banco de dados primário substituído.  
  
     Para obter mais informações, veja [Backups de log do transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).   
  
4.  Depois que os servidores secundários forem sincronizados, você poderá fazer o failover para o banco de dados que preferir recuperando o banco de dados secundário e redirecionando os clientes para aquela instância de servidor. A recuperação coloca o banco de dados em um estado consistente e online.  
  
    > [!NOTE]  
    >  Ao disponibilizar um banco de dados secundário, você deve assegurar que os metadados estejam consistentes com os metadados do banco de dados primário original. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
5.  Depois de recuperar um banco de dados secundário, você poderá reconfigurá-lo para que atue como um banco de dados primário para outros bancos de dados secundários.  
  
     Se nenhum outro banco de dados secundário estiver disponível, veja [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Alterar funções entre servidores de envio de log primários e secundários &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [Gerenciamento de logons e trabalhos após a troca de funções &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
