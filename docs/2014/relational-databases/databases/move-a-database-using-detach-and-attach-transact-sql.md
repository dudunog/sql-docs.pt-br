---
title: Mover um banco de dados utilizando Desanexar e Anexar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- moving databases [SQL Server]
- database detaching [SQL Server]
- relocating databases [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 6732a431-cdef-4f1e-9262-4ac3b77c275e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16fa57c35c2c40d307b73809c21ccfbedc54f705
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917075"
---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>Mover um banco de dados utilizando Desanexar e Anexar (Transact-SQL)
  Este tópico descreve como mover um banco de dados desanexado para outro local e anexá-lo novamente à mesma instância de servidor ou a uma instância diferente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No entanto, recomendamos que você mova os bancos de dados utilizando o procedimento de realocação planejada ALTER DATABASE, em vez de utilizar desanexar e anexar. Para obter mais informações, veja [Mover bancos de dados de usuário](move-user-databases.md).  
  
> [!IMPORTANT]  
>  Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>Para mover um banco de dados usando anexar e desanexar  
  
1.  Desanexe o banco de dados. Para obter mais informações, veja [Desanexar um banco de dados](detach-a-database.md).  
  
2.  Em uma janela do Windows Explorer ou do prompt de comando do Windows, mova os arquivos do banco de dados desanexado e os arquivos de log para o novo local.  
  
    > [!NOTE]  
    >  Para mover um banco de dados de um único arquivo, você poderá utilizar email se o tamanho do arquivo for pequeno o bastante para caber no email.  
  
     Você deverá mover os arquivos de log, mesmo se pretender criar novos arquivos de log. Em alguns casos, reanexar um banco de dados exige seus arquivos de log existentes. Portanto, mantenha todos os arquivos de log desanexados até que o banco de dados seja anexado com êxito sem eles.  
  
    > [!NOTE]  
    >  Se você tentar anexar o banco de dados sem especificar o arquivo de log, a operação de anexação procurará o arquivo de log em seu local original. Se ainda existir uma cópia do log no local original, essa cópia será anexada. Para evitar a utilização do arquivo de log original, especifique o caminho do novo arquivo de log ou remova a cópia original do arquivo de log (depois de copiá-la para o novo local).  
  
3.  Anexe os arquivos copiados. Para obter mais informações, consulte [Attach a Database](attach-a-database.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria uma cópia das [!INCLUDE[ssSampleDBnormal](../../includes/tsql-md.md)] instruções que são executadas em uma janela do editor de consultas que está conectada à instância do servidor à qual está anexada.  
  
1.  Desanexe [!INCLUDE[ssSampleDBnormal](../../includes/tsql-md.md)] as instruções:  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'AdventureWorks2012';  
    GO  
    ```  
  
2.  Utilizando o método de sua preferência, copie os arquivos de banco de dados (AdventureWorks208R2_Data.mdf e AdventureWorks208R2_log) para C:\MySQLServer\AdventureWorks208R2_Data.mdf e C:\MySQLServer\AdventureWorks208R2_Log.ldf, respectivamente.  
  
    > [!IMPORTANT]  
    >  Para um banco de dados de produção, coloque o banco de dados e o log de transações em discos separados.  
  
     Para copiar arquivos pela rede para um disco ou um computador remoto, utilize o nome UNC (Convenção Universal de Nomenclatura) do local remoto. Um nome UNC possui o formato **\\\\** _Servername_ **\\** _Sharename_ **\\** _Path_ **\\** _Filename_. Assim como ocorre com a gravação de arquivos no disco rígido local, deverão ser concedidas, à conta do usuário utilizada pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as permissões apropriadas exigidas para ler ou gravar em um arquivo no disco remoto.  
  
3.  Anexe o banco de dados movido e, opcionalmente, seu log executando as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Data.mdf'),  
        (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Log.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um banco de dados anexado recentemente não fica imediatamente visível no Pesquisador de Objetos. Para exibir o banco de dados, no Pesquisador de Objetos, clique em **Exibir** e depois em **Atualizar**. Quando o nó **Bancos de Dados** for expandido no Pesquisador de Objetos, o banco de dados recentemente anexado será exibido na lista de bancos de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
