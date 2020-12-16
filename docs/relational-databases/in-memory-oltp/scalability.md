---
title: Escalabilidade | Microsoft Docs
description: Saiba mais sobre os aprimoramentos na escalabilidade para o armazenamento em disco de tabelas com otimização de memória no SQL Server, como o uso de vários threads para persistir tabelas.
ms.custom: ''
ms.date: 08/27/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 251af732e6c55ee2b5567bb181859b1fdec1360a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485218"
---
# <a name="scalability"></a>Escalabilidade
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] contém aprimoramentos de escalabilidade para o armazenamento em disco de tabelas com otimização de memória. 

## <a name="multiple-threads-to-persist-memory-optimized-tables"></a>Vários threads para manter tabelas com otimização de memória  
  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tinha um único thread de ponto de verificação offline que verificava o log de transações em busca de alterações em tabelas com otimização de memória e que as mantinha em arquivos de ponto de verificação (como arquivos delta e de dados). Em computadores com um número maior de núcleos, o thread de ponto de verificação offline único poderia ficar para trás.  
  
Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], há vários threads simultâneos responsáveis por manter as alterações nas tabelas com otimização de memória.  
  
## <a name="multi-threaded-recovery"></a>Recuperação com multithread
Na versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a aplicação de log como parte da operação de recuperação era single-threaded. Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a aplicação de log é multi-threaded.  
  
## <a name="merge-operation"></a>Operação MERGE  
Agora, a operação MERGE é multi-threaded.  
   
> [!NOTE]
> A Mesclagem Manual foi desabilitada, pois espera-se que a mesclagem multi-threaded acompanhe a carga. 

## <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico  
Houve alterações significativas em [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) e [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) dos DMVs.  

## <a name="storage-management"></a>Gerenciamento de armazenamento
O mecanismo OLTP na Memória continua a usar o grupo de arquivos com otimização de memória com base no FILESTREAM, mas o grupo de arquivos individuais é separado do FILESTREAM. Esses arquivos são totalmente gerenciados (para criação, remoção e coleta de lixo) pelo mecanismo de OLTP na Memória. 

> [!NOTE]
> Não há suporte para [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também   
[Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)     
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[Opções de arquivo e grupos de arquivos ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)    
