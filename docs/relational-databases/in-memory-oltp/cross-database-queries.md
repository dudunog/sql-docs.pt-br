---
title: Consultas de bancos de dados | Microsoft Docs
description: Saiba como usar as variáveis de tabela com otimização de memória em consultas entre bancos de dados para mover dados de um banco de dados para tabelas com otimização de memória no SQL Server.
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b73ea09a24e2091a76d6bf2526c1f7a17e3afd60
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868003"
---
# <a name="cross-database-queries"></a>Consultas de bancos de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], as tabelas com otimização de memória não oferecem suporte a transações envolvendo todos os bancos de dados. Você não pode acessar outro banco de dados da mesma transação ou na mesma consulta que também acesse uma tabela com otimização de memória. Você não pode copiar facilmente dados de uma tabela em um banco de dados, para uma tabela com otimização de memória em outro banco de dados.  
  
 Variáveis de tabela não são transacionais. Assim, as variáveis de tabela com otimização de memória podem ser usadas em consultas de bancos de dados e, portanto, podem facilitar a movimentação de dados de um banco de dados para tabelas com otimização de memória em outro. Você pode usar duas transações. Na primeira transação, insira os dados da tabela remota na variável. Na segunda transação, insira os dados na tabela com otimização de memória local da variável.  Para obter mais informações sobre variáveis de tabela com otimização de memória, consulte [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
## <a name="example"></a>Exemplo
Este exemplo ilustra um método para transferir dados de um banco de dados para uma tabela com otimização de memória em um banco de dados diferente.

1. Crie objetos de teste.  Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  

    ```sql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  Tente realizar consultas entre bancos de dados. Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
  
    ```sql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    Você deve receber a seguinte mensagem de erro:
    > Msg 41317, Nível 16, Estado 5  
    > Uma transação de utilizador que aceda a tabelas com otimização de memória ou módulos compilados nativamente não pode aceder a mais de uma base de dados de utilizador ou um modelo de bases de dados e msdb e não pode escrever na mestra.

3.  Crie uma tabela com otimização de memória.  Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

    ```sql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  Tente realizar novamente as consultas entre bancos de dados.  Desta vez, os dados de origem serão transferidos primeiro para uma variável de tabela com otimização de memória.  Em seguida, os dados da variável de tabela serão transferidos para a tabela com otimização de memória.
    ```sql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
