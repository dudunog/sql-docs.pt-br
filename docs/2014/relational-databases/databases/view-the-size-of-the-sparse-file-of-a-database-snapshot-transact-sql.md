---
title: Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2a7e507e45d8429312834911b7bef5ae1e784c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870875"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados (Transact-SQL)
  Este tópico descreve como usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para verificar se um arquivo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um arquivo esparso e descobrir seu tamanho real e máximo. Arquivos esparsos, que são um recurso do sistema de arquivos NTFS, são usados por instantâneos do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Durante a criação do instantâneo do banco de dados, arquivos esparsos são criados usando os nomes de arquivo na instrução CREATE DATABASE. Esses nomes de arquivo são armazenados em **sys.master_files** na coluna **physical_name** . Em **sys.database_files** (quer seja no banco de dados de origem ou em um instantâneo), a coluna **physical_name** sempre contém os nomes dos arquivos de banco de dados de origem.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>Verificar se um arquivo de banco de dados é um arquivo esparso  
  
1.  Na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Selecione a coluna **is_sparse** de **sys.database_files** no instantâneo do banco de dados ou de **sys.master_files**. O valor indica se o arquivo é um arquivo esparso, como segue:  
  
     1 = O arquivo é um arquivo esparso.  
  
     0 = O arquivo não é um arquivo esparso.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>Descobrir o tamanho real de um arquivo esparso  
  
> [!NOTE]  
>  Arquivos esparsos crescem em incrementos de 64 KB (quilobyte); portanto, o tamanho de um arquivo esparso no disco sempre é um múltiplo de 64 KB.  
  
 Para exibir o número de bytes que cada arquivo esparso de um instantâneo está usando no disco no momento, consulte a coluna **size_on_disk_bytes** da exibição de gerenciamento dinâmico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][sys.dm_io_virtual_file_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql).  
  
 Para exibir o espaço em disco usado por um arquivo esparso, clique com o botão direito do mouse no Microsoft Windows, clique em **Propriedades**e examine o valor de **Tamanho em disco** .  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>Descobrir o tamanho máximo de um arquivo esparso  
 O tamanho máximo de crescimento de um arquivo esparso é o tamanho do arquivo de banco de dados de origem correspondente, no momento da criação do instantâneo. Para saber qual é este tamanho, você pode usar uma das alternativas seguintes:  
  
-   Usando o prompt de comando do Windows:  
  
    1.  Use os comandos **dir** do Windows.  
  
    2.  Selecione o arquivo esparso, abra a caixa de diálogo **Propriedades** do arquivo no Windows, e consulte o valor **Tamanho** .  
  
-   Na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Selecione a coluna **size** em **sys.database_files** no instantâneo do banco de dados ou em **sys.master_files**. O valor da coluna **size** reflete o espaço máximo, em páginas SQL, que o instantâneo pode vir a usar; esse valor é equivalente ao campo **Tamanho** do Windows, a não ser que seja representado em número de páginas SQL no arquivo; o tamanho em bytes é:  
  
     ( *number_of_pages* * 8192)  
  
## <a name="see-also"></a>Consulte Também  
 [Instantâneos do banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [sys. fn_virtualfilestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [sys. database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
