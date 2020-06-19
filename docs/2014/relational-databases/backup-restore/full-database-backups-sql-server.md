---
title: Backups de bancos de dados completos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- backups [SQL Server], database
- backing up databases [SQL Server], full backups
- estimating database backup size
- backing up [SQL Server], size of backup
- database backups [SQL Server], full backups
- size [SQL Server], backups
- database backups [SQL Server], about backing up databases
ms.assetid: 4d933d19-8d21-4aa1-8153-d230cb3a3f99
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ee871b6cabbe6c2b2cb4f444fd1e2d42d711dfbc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84957969"
---
# <a name="full-database-backups-sql-server"></a>Backups de bancos de dados completos (SQL Server)
  Um backup completo de banco de dados faz o backup de todo o banco de dados. Isso inclui parte do log de transações de modo que o banco de dados completo possa ser recuperado depois que um backup completo de banco de dados for restaurado. Backups completos de banco de dados representam o banco de dados no momento em que o backup foi concluído.  
  
> [!TIP]  
>  À medida que um banco de dados aumenta, os backups completos de banco de dados levam mais tempo para serem concluídos e exigem mais espaço de armazenamento. Portanto, para um banco de dados grande, convém complementar um backup de banco de dados completo com uma série de *backups de bancos de dados diferenciais*. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
> [!IMPORTANT]  
>  TRUSTWORTHY é definido como OFF em um backup de banco de dados. Para obter informações sobre como definir TRUSTWORTHY como ON, veja [Opções do ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 **Neste tópico:**  
  
-   [Backups de banco de dados no modelo de recuperação simples](#DbBuRMs)  
  
-   [Backups de banco de dados no modelo de recuperação completa](#DbBuRMf)  
  
-   [Usar um backup de banco de dados completo para restaurar o banco de dados](#RestoreDbBu)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="database-backups-under-the-simple-recovery-model"></a><a name="DbBuRMs"></a> Backups de banco de dados no modelo de recuperação simples  
 No modelo de recuperação simples, depois de cada backup, o banco de dados fica sujeito à possível perda de trabalho na eventualidade de um desastre. A possibilidade de perda de trabalho aumenta a cada atualização até que o próximo backup seja feito, quando a possibilidade de perda de trabalho retorna a zero, tendo início um novo ciclo de exposição à perda de trabalho. A possibilidade de perda de trabalho aumenta com o passar do tempo entre os backups. A ilustração a seguir mostra a exposição à perda de trabalho de uma estratégia de backup que usa apenas backups de banco de dados completos.  
  
 ![Mostra a exposição da perda de trabalho entre backups de banco de dados](../../database-engine/media/bnr-rmsimple-1-fulldb-backups.gif "Mostra a exposição da perda de trabalho entre backups de banco de dados")  
  
### <a name="example--tsql"></a>Exemplo ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 O exemplo a seguir mostra como criar um backup de banco de dados completo usando WITH FORMAT para substituir qualquer backup existente e criar um novo conjunto de mídias.  
  
```  
-- Back up the AdventureWorks2012 database to new media set.  
BACKUP DATABASE AdventureWorks2012  
    TO DISK = 'Z:\SQLServerBackups\AdventureWorksSimpleRM.bak'   
    WITH FORMAT;  
GO  
```  
  
##  <a name="database-backups-under-the-full-recovery-model"></a><a name="DbBuRMf"></a> Backups de banco de dados no modelo de recuperação completa  
 Para bancos de dados que usam recuperação completa e recuperação bulk-logged, os backups de banco de dados são necessários, mas não são suficientes. Os backups de log de transações também são necessários. A ilustração a seguir mostra a estratégia de backup menos complexa possível no modelo de recuperação completa.  
  
 ![Séries de backups de bancos de dados e backups de log completos](../../database-engine/media/bnr-rmfull-1-fulldb-log-backups.gif "Séries de backups de bancos de dados e backups de log completos")  
  
 Para obter informações sobre como criar backups de logs, veja [Backups do log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
### <a name="example--tsql"></a>Exemplo ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 O exemplo a seguir mostra como criar um backup de banco de dados completo usando WITH FORMAT para substituir qualquer backup existente e criar um novo conjunto de mídias. Assim, o exemplo faz o backup do log de transações. Em uma situação da vida real, você teria de executar uma série de backups regulares de log. Para esse exemplo, o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] deve ser definido para usar o modelo de recuperação completa.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
-- Back up the AdventureWorks2012 database to new media set (backup set 1).  
BACKUP DATABASE AdventureWorks2012  
  TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak'   
  WITH FORMAT;  
GO  
--Create a routine log backup (backup set 2).  
BACKUP LOG AdventureWorks2012 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak';  
GO  
```  
  
##  <a name="use-a-full-database-backup-to-restore-the-database"></a><a name="RestoreDbBu"></a> Usar um backup de banco de dados completo para restaurar o banco de dados  
 É possível recriar todo o banco de dados de uma só vez, restaurando o banco de dados a partir de um backup completo de banco de dados para qualquer local. Uma parte suficiente do log de transações é incluída no backup para permitir que você recupere o banco de dados até o momento em que o backup foi concluído. O banco de dados restaurado equivale ao estado do banco de dados original quando o backup de banco de dados é concluído, desconsiderando transações não confirmadas. No modelo de recuperação completa, você deve restaurar todos os backups de log de transações subsequentes. Quando o banco de dados é recuperado, as transações não confirmadas são revertidas.  
  
 Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md) ou [Restaurações completas de banco de dados &#40;Modelo de recuperação completa#41;](complete-database-restores-full-recovery-model.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para criar um backup de banco de dados completo**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 **Para agendar trabalhos de backup**  
  
 [Usar o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup e restaurar bancos de dados do SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Backup e restauração de bancos de dados do Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)  
  
  
