---
title: Definir backup ou restauração após o erro
description: Saiba como especificar se uma operação de backup ou restauração continua após encontrar um erro no SQL Server usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], backups
- backing up databases [SQL Server], errors
- backups [SQL Server], errors
- database backups [SQL Server], errors
ms.assetid: 042be17a-b9b0-4629-b6bb-b87a8bc6c316
author: cawrites
ms.author: chadam
ms.openlocfilehash: cddc94d853dffef5e030ccc388c0b95bbc5f745a
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129055"
---
# <a name="specify-backup-or-restore-to-continue-or-stop-after-error"></a>Especifique backup ou restauração para continuar ou parar após o erro
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como especificar se uma operação de backup ou restauração continuará ou será interrompida após encontrar um erro no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para especificar se uma operação de backup ou restauração continua depois de encontrar um erro usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 BACKUP  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
 RESTORE  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-specify-whether-backup-continues-or-stops-after-an-error-is-encountered"></a>Para especificar se o backup para ou continua depois de encontrar um erro  
  
1.  Siga as etapas para [criar um backup de banco de dados](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Na página **Opções** , na seção **Confiabilidade** , clique em **Executar soma de verificação antes de gravar na mídia** e em **Continuar se houver erro**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-specify-whether-a-backup-operation-continues-or-stops-after-encountering-an-error"></a>Para especificar se uma operação de backup para ou continua depois de encontrar um erro  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Na instrução [BACKUP](../../t-sql/statements/backup-transact-sql.md) , especifique a opção CONTINUE_AFTER ERROR para continuar ou a opção STOP_ON_ERROR para parar. O comportamento padrão é parar depois de encontrar um erro. Este exemplo instrui a operação de backup a continuar apesar de encontrar um erro.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
#### <a name="to-specify-whether-a-restore-operation-continues-or-stops-after-encountering-an-error"></a>Para especificar se uma operação de restauração para ou continua depois de encontrar um erro  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Na instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) , especifique a opção CONTINUE_AFTER ERROR para continuar ou a opção STOP_ON_ERROR para parar. O comportamento padrão é parar depois de encontrar um erro. Este exemplo instrui a operação de restauração a continuar apesar de encontrar um erro.  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'   
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [Habilitar ou desabilitar as somas de verificação de backup durante backup ou restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
  
