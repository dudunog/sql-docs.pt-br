---
title: Suporte ao Transact-SQL para OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c8f67f3745ea4dfc4aa1b37f5b681b14a4b608ba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68081822"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Suporte ao Transact-SQL para OLTP na memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  As seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] incluem opções de sintaxe para dar suporte ao OLTP in-memory:  
  
-   [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) (adição de **MEMORY_OPTIMIZED_DATA**)  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) (adição de **MEMORY_OPTIMIZED_DATA**)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
    Em um procedimento armazenado compilado de modo nativo, você pode declarar uma variável como **NOT NULL**. Não é possível fazer isso em um procedimento armazenado normal.  
  
 **AUTO_UPDATE_STATISTICS** pode ser **ON** para tabelas com otimização de memória, a partir do SQL Server 2016. Para obter mais informações, veja [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md).  
  
 Não há suporte para [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md) ON em procedimentos armazenados compilados de modo nativo.  
  
 Para obter informações sobre os recursos sem suporte, veja [Construções do Transact-SQL sem suporte pelo OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Para obter informações sobre as construções com suporte em procedimentos armazenados compilados de modo nativo, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md) e [DDL com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md).  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Recursos do SQL Server sem suporte para OLTP na Memória](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
