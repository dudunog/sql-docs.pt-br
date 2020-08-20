---
description: Mover bancos de dados de usuário
title: Mover bancos de dados de usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- editions [SQL Server], moving databases between
- moving full-text catalogs
- scheduled disk maintenace [SQL Server]
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- moving user databases
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: ad9a4e92-13fb-457d-996a-66ffc2d55b79
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0892e0a2a6db25e6a82f56177544572b8a5af388
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471204"
---
# <a name="move-user-databases"></a>Mover bancos de dados de usuário
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível mover os dados, o log e os arquivos de catálogo de texto completo de um banco de dados de usuário para um novo local, especificando o novo local do arquivo na cláusula FILENAME da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) . Esse método é aplicado para mover arquivos do banco de dados dentro da mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para mover um banco de dados para uma outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para um outro servidor, use as operações de [backup e restauração](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) ou [anexar e desanexar](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md).  
  
## <a name="considerations"></a>Considerações  
 Ao mover um banco de dados para outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, talvez seja necessário recriar alguns ou todos os metadados do banco de dados. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 Alguns recursos do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] alteram a maneira como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena as informações nos arquivos de banco de dados. Esses recursos são restritos a edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um banco de dados que contém esses recursos não pode ser movido para uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dê suporte a eles. Use a exibição de gerenciamento dinâmico sys.dm_db_persisted_sku_features para listar todos os recursos específicos de edição habilitados no banco de dados atual.  
  
 Os procedimentos neste tópico exigem o nome lógico dos arquivos de banco de dados. Para obter o nome, consulte a coluna de nome na exibição de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) .  
  
 A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], os catálogos de texto completo são integrados no banco de dados em vez de serem armazenados no sistema de arquivos. Os catálogos de texto completo agora são movidos automaticamente quando você move um banco de dados.  
  
## <a name="planned-relocation-procedure"></a>Procedimento de realocação planejada  
 Para mover um arquivo de dados ou de log como parte de uma realocação planejada, execute as seguintes etapas:  
  
1.  Execute a seguinte instrução.  
  
    ```  
    ALTER DATABASE database_name SET OFFLINE;  
    ```  
  
2.  Mova o arquivo ou os arquivos para o novo local.  
  
3.  Para cada arquivo movido, execute a seguinte instrução.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name, FILENAME = 'new_path\os_file_name' );  
    ```  
  
4.  Execute a seguinte instrução.  
  
    ```  
    ALTER DATABASE database_name SET ONLINE;  
    ```  
  
5.  Execute a consulta a seguir para verificar se houve alteração no arquivo.  

    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="relocation-for-scheduled-disk-maintenance"></a>Realocação para manutenção de disco programada  
 Para realocar um arquivo como parte de um processo de manutenção de disco programada, execute as seguintes etapas:  
  
1.  Para cada arquivo a ser movido, execute a seguinte instrução.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
2.  Pare a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou desligue o sistema para realizar a manutenção. Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Mova o arquivo ou os arquivos para o novo local.  
  
4.  Reinicialize a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o servidor. Para obter mais informações, veja [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
5.  Execute a consulta a seguir para verificar se houve alteração no arquivo.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="failure-recovery-procedure"></a>Falha no procedimento de recuperação  
 Se um arquivo tiver que ser movido devido à uma falha de hardware, execute as seguintes etapas para realocar o arquivo no novo local.  
  
> [!IMPORTANT]  
>  Se o banco de dados não puder ser inicializado, significa que ele está em modo de suspeição ou em estado não recuperado, e apenas os membros de função fixa sysadmin podem mover o arquivo.  
  
1.  Interrompa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se tiver sido iniciado.  
  
2.  Inicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo somente recuperação mestre, inserindo um dos seguintes comandos no prompt de comando.  
  
    -   Para a instância padrão (MSSQLSERVER), execute o seguinte comando.  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   Para uma instância nomeada, execute o seguinte comando.  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Para cada arquivo a ser movido, use comandos **sqlcmd** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para executar a instrução a seguir.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
     Para obter mais informações sobre como usar o utilitário **sqlcmd** , veja [Usar o Utilitário sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
4.  Saia do utilitário **sqlcmd** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
5.  Pare a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Mova o arquivo ou os arquivos para o novo local.  
  
7.  Inicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, execute `NET START MSSQLSERVER`.  
  
8.  Execute a consulta a seguir para verificar se houve alteração no arquivo.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte move o arquivo de log [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para um novo local como parte de uma realocação planejada.  
  
```  
USE master;  
GO  
-- Return the logical file name.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
GO  
ALTER DATABASE AdventureWorks2012 SET OFFLINE;  
GO  
-- Physically move the file to a new location.  
-- In the following statement, modify the path specified in FILENAME to  
-- the new location of the file on your server.  
ALTER DATABASE AdventureWorks2012   
    MODIFY FILE ( NAME = AdventureWorks2012_Log,   
                  FILENAME = 'C:\NewLoc\AdventureWorks2012_Log.ldf');  
GO  
ALTER DATABASE AdventureWorks2012 SET ONLINE;  
GO  
--Verify the new location.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md)   
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
