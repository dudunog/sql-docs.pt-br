---
title: Modelos de recuperação (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- bulk-logged recovery model [SQL Server]
- recovery [SQL Server], recovery model
- restoring transaction logs [SQL Server], recovery models
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], about
- transaction log backups [SQL Server]
- simple recovery model [SQL Server]
- backups [SQL Server], recovery models
- recovery models [SQL Server]
- recovery models [SQL Server], transaction log management
- database restores [SQL Server], recovery models
- transaction log restores [SQL Server]
- logs [SQL Server], recovery models
- restoring databases [SQL Server], recovery models
- full recovery model [SQL Server]
- backing up transaction logs [SQL Server], recovery models
ms.assetid: 8cfea566-8f89-4581-b30d-c53f1f2c79eb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5b85e316c859e0b6d44fb83e3df6da2edd72ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62921761"
---
# <a name="recovery-models-sql-server"></a>Modelos de recuperação (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as operações de backup e restauração ocorrem no contexto do modelo de recuperação do banco de dados. Os modelos de recuperação são projetados para controlar a manutenção de log de transações. Um *modelo de recuperação* é uma propriedade de banco de dados que controla como as transações são registradas, se o log de transações exige (e permite) backup e que tipos de operações de restauração estão disponíveis. Existem três modelos de recuperação: simples, completo e bulk-logged. Geralmente, um banco de dados usa o modelo de recuperação completa ou o modelo de recuperação simples. É possível alternar para outro modelo de recuperação do banco de dados a qualquer momento.  
  
 **Neste tópico:**  
  
-   [Visão geral do modelo de recuperação](#RMov)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="recovery-model-overview"></a><a name="RMov"></a> Visão geral do modelo de recuperação  
 A tabela a seguir resume os três modelos de recuperação.  
  
|modelo de recuperação|DESCRIÇÃO|Exposição à perda de trabalho|Recuperação pontual?|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**Simples**|Sem backups de log<br /><br /> Reclama espaço de log automaticamente para manter requisitos de espaços pequenos, eliminando essencialmente a necessidade de gerenciar o espaço de log de transações. Para obter informações sobre backups de banco de dados no modelo de recuperação simples, veja [Backups completos de banco de dados &#40;SQL Server&#41;](full-database-backups-sql-server.md).<br /><br /> As operações que exigem backups de log de transações não têm suporte no modelo de recuperação simples. Os recursos a seguir não podem ser usados no modo de recuperação simples:<br /><br /> Envio de logs<br /><br /> AlwaysOn ou espelhamento de banco de dados<br /><br /> Recuperação de mídia sem perda de dados<br /><br /> Restaurações em um momento determinado|As alterações desde o backup mais recente estão desprotegidas. No caso de um desastre, essas alterações devem ser refeitas.|Só pode recuperar até o fim de um backup. Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples&#41;](complete-database-restores-simple-recovery-model.md).|  
|**Completo**|Requer backups de log.<br /><br /> Nenhum trabalho é perdido devido a um arquivo de dados perdido ou danificado.<br /><br /> Pode executar uma recuperação pontual (por exemplo, antes de um erro de aplicativo ou usuário). Para obter informações sobre backups de banco de dados no modelo de recuperação completa, veja [Backups completos de banco de dados &#40;SQL Server&#41;](full-database-backups-sql-server.md) e [Restaurações completas de banco de dados &#40;Modelo de recuperação completo&#41;](complete-database-restores-full-recovery-model.md).|Geralmente nenhum.<br /><br /> Se a parte final do log estiver danificada, as alterações desde o backup de log mais recente deverão ser refeitas.|Pode executar uma recuperação pontual, supondo que seus backups estejam concluídos até aquele ponto. Para obter informações sobre como usar backups de log para restaurar no ponto de falha, veja [Restaurar um Banco de dados SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).<br /><br /> Observação: se você tiver dois ou mais bancos de dados de modelo de recuperação completa que devem ser logicamente consistentes, é possível que você precise implementar procedimentos especiais para verificar a possibilidade de recuperação desses bancos de dados. Para obter mais informações, veja [Recuperação de bancos de dados relacionados que contêm transação marcada](recovery-of-related-databases-that-contain-marked-transaction.md).|  
|**Bulk-logged**|Requer backups de log.<br /><br /> Um suplemento do modelo de recuperação completa que permite operações de cópia em massa de alto desempenho.<br /><br /> Reduz o uso de espaços de log usando o mínimo de registro em log para a maioria das operações em massa. Para obter informações sobre as operações que podem ser minimamente registradas, veja [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).<br /><br /> Para obter informações sobre backups de banco de dados no modelo de recuperação bulk-logged, veja [Backups completos de banco de dados &#40;SQL Server&#41;](full-database-backups-sql-server.md) e [Restaurações completas de banco de dados &#40;Modelo de recuperação completo&#41;](complete-database-restores-full-recovery-model.md).|Se o log estiver danificado ou se ocorreu registro de operações em massa desde o backup de log mais recente, as alterações desde o último backup deverão ser refeitas.<br /><br /> Caso contrário, nenhum trabalho será perdido.|Pode recuperar até o final de qualquer backup. Não há suporte para recuperação pontual.|  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;do conjunto de backup &#40;Transact-SQL](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [Backup e restauração de bancos de dados SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
