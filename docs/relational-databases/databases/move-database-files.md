---
description: Mover arquivos de banco de dados
title: Mover arquivos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa8fe0e721bbe571cf1f47d95bfdd79029059846
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194299"
---
# <a name="move-database-files"></a>Mover arquivos de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível mover bancos de dados de usuários e sistemas especificando o novo local do arquivo na cláusula FILENAME da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). É possível mover arquivos de dados, logs e catálogos de texto completo deste modo. Isso pode ser útil nas seguintes situações:  
  
-   Recuperação de falha. Por exemplo, o banco de dados está em modo suspeito ou foi fechado por causa de um problema de hardware.  
  
-   Realocação planejada.  
  
-   Realocação para manutenção de disco programada.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de usuários e arquivos de catálogo de texto completo para um local novo.|  
|[Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de sistema para um novo local.|  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
