---
title: Backup gerenciado – configurar opções avançadas
description: Este tutorial descreve como definir as opções avançadas do Backup Gerenciado do SQL Server para o Microsoft Azure, caso as opções padrão não atendam às suas necessidades.
titleSuffix: to Microsoft Azure
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1e49a379ed12123c684497d84804c9ebd1ebf9ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748472"
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Configurar opções avançadas de backup gerenciado do SQL Server para o Microsoft Azure
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O tutorial a seguir descreve como definir opções avançadas para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Esses procedimentos só serão necessários se você precisar dos recursos que oferecem. Caso contrário, você pode habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e depender do comportamento padrão.  
  
 Em cada cenário, o backup é especificado usando o parâmetro `database_name` . Quando `database_name` é NULL ou *, as alterações afetam as configurações padrão no nível da instância. Configurações de nível de instância também afetam os novos bancos de dados criados após a alteração.  
  
 Depois de especificar essas configurações, será possível habilitar o backup gerenciado para o banco de dados ou a instância usando o procedimento armazenado do sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Para obter mais informações, veja [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
> [!WARNING]  
>  Você sempre deve configurar as opções avançadas e as opções de agendamento personalizado antes de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Caso contrário, é possível que operações de backup não desejadas ocorram durante a janela de tempo entre a habilitação do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e a definição dessas configurações.  
  
## <a name="configure-encryption"></a>Configurar a criptografia  
 As etapas a seguir descrevem como especificar as configurações de criptografia usando o procedimento armazenado [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md).  

1.  **Determine o algoritmo de criptografia:** primeiro determine o nome do algoritmo de criptografia a ser usado. Selecione um dos seguintes algoritmos.  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **Criar uma chave mestra de banco de dados:** Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **Para criar um certificado de backup ou uma chave assimétrica:** você pode usar um certificado ou uma chave assimétrica com a criptografia. O exemplo a seguir cria um certificado de backup a ser usado na criptografia.  
  
    ```sql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **Definir criptografia de backup gerenciado:** chame o procedimento armazenado **managed_backup.sp_backup_config_advanced** com os valores correspondentes. Por exemplo, o exemplo a seguir configura o banco de dados `MyDB` para criptografia usando um certificado denominado `MyTestDBBackupEncryptCert` e o algoritmo de criptografia `AES_128` .  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  Se `@database_name` for NULL no exemplo anterior, as configurações se aplicarão à instância do SQL Server.  
  
## <a name="configure-a-custom-backup-schedule"></a>Configurar um agendamento de backup personalizado  
 As etapas a seguir descrevem como definir um agendamento personalizado com o procedimento armazenado [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md).  
  
1.  **Determine a frequência de backups completos:** determine a frequência de backups completos do banco de dados. Você pode escolher entre backups completos “Diariamente” e “Semanalmente”.  
  
2.  **Determine a frequência de backups de log de transações:** Determine a frequência de backup de log de transações. Esse valor é em minutos ou horas.  
  
3.  **Determine o dia da semana dos backups semanais:** se o backup for semanal, escolha um dia da semana para o backup completo.  
  
4.  **Determine a hora de início do backup:** usando a notação de 24 horas, escolha um horário para iniciar o backup.  
  
5.  **Determine o período de tempo para permitir o backup:** Isso especifica a quantidade de tempo que um backup tem para ser concluído.  
  
6.  **Definir o agendamento de backup personalizado:** o procedimento armazenado a seguir define um agendamento personalizada para o banco de dados `MyDB`. Backups completos são realizados semanalmente em `Monday` às `17:30`. Backups de log são executados a cada `5` minutos. Os backups têm duas horas para serem concluídos.  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de configurar opções avançadas e agendas personalizadas, é necessário habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no banco de dados de destino ou instância do SQL Server. Para obter mais informações, veja [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Backup Gerenciado do SQL Server para o Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
