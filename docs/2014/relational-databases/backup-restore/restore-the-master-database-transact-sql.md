---
title: Restaurar o banco de dados mestre (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7c9cb078b7af60fc5e060bcb144fc9cbaee8ecf7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956676"
---
# <a name="restore-the-master-database-transact-sql"></a>Restaurar o banco de dados mestre (Transact-SQL)
  Este tópico explica como restaurar o banco de dados **master** com base em um backup de banco de dados completo.  
  
### <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie uma instância de servidor no modo de usuário único.  
  
     Para obter informações sobre como especificar o parâmetro de inicialização de usuário único ( **-m**), veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Para restaurar um backup de banco de dados completo do **master**, use a seguinte instrução [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *<backup_device>*  `WITH REPLACE`  
  
     A opção REPLACE instrui o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a restaurar o banco de dados especificado mesmo quando um banco de dados do mesmo nome já existir. O banco de dados existente, se houver, será excluído. Em modo de usuário único, é recomendável inserir a instrução RESTORE DATABASE no [utilitário sqlcmd](../../tools/sqlcmd-utility.md). Para obter mais informações, consulte [Usar o Utilitário sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  Depois que o **master** é restaurado, a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é encerrada e o processo **sqlcmd** é concluído. Antes de reiniciar a instância do servidor, remova o parâmetro de inicialização de usuário único. Para obter mais informações, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Reinicie a instância do servidor e continue outras etapas de recuperação, como restaurar outros bancos de dados, anexar bancos de dados e corrigir incompatibilidades de usuário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir restaura o banco de dados `master` na instância do servidor padrão. O exemplo assume que a instância do servidor já está sendo executada no modo de usuário único. O exemplo inicia o `sqlcmd` e executa uma instrução `RESTORE DATABASE` que restaura um backup de banco de dados completo de `master` de um dispositivo de disco: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]
>  Para uma instância nomeada, o comando **sqlcmd** deve especificar a opção **-S** _\<ComputerName>_ \\ *\<InstanceName>* .  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)   
 [Recriar bancos de dados do sistema](../databases/system-databases.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
