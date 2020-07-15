---
title: Estados de banco de dados | Microsoft Docs
description: Saiba mais sobre vários estados de banco de dados, como ONLINE, OFFLINE ou SUSPECT. Saiba como verificar o estado atual de um banco de dados.
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4c75323d843fd260c1e6228d7ae73d382e4f9462
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002972"
---
# <a name="database-states"></a>Estados de banco de dados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Um banco de dados sempre está em um estado específico. Por exemplo, esses estados incluem ONLINE, OFFLINE ou SUSPECT. Para verificar o estado atual de um banco de dados, selecione a coluna **state_desc** na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou a propriedade **Status** da função [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) .  
  
## <a name="database-state-definitions"></a>Definições de estado de banco de dados  
 A tabela a seguir define os estados de banco de dados.  
  
|Estado|Definição|  
|-----------|----------------|  
|ONLINE|O banco de dados está disponível para acesso. O grupo de arquivos primário está on-line, embora a fase desfazer de recuperação pode não ter sido completada.|  
|OFFLINE|O banco de dados está indisponível. Um banco de dados se torna off-line por ação explícita do usuário e permanece off-line até que uma ação adicional do usuário seja executada. Por exemplo, o banco de dados pode ser ficar off-line para que um arquivo seja movido para um novo disco. O banco de dados é, então, colocado on-line novamente, após a mudança ter sido concluída.|  
|RESTORING|Um ou mais arquivos do grupo de arquivos primário está sendo restaurado ou um ou mais arquivos secundários está sendo restaurado off-line. O banco de dados está indisponível.|  
|RECOVERING|O banco de dados está sendo recuperado. O processo de recuperação é um estado transitório, o banco de dados ficará on-line automaticamente se a recuperação for bem-sucedida. Se a recuperação falhar, o banco de dados se tornará suspeito. O banco de dados está indisponível.|  
|RECOVERY_PENDING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou um erro relacionado a recurso durante a recuperação. O banco de dados não está danificado, mas arquivos podem ter sido perdidos ou limitações de recursos do sistema podem estar impedindo sua inicialização. O banco de dados está indisponível. Uma ação adicional é exigida do usuário para resolver o erro e permitir que o processo de recuperação seja concluído.|  
|SUSPECT|Pelo menos o grupo de arquivos primário é suspeito e pode estar danificado. O banco de dados não pode ser recuperado durante a inicialização de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados está indisponível. Ação adicional pelo usuário é exigida para resolver o problema.|  
|EMERGENCY|O usuário alterou o banco de dados e definiu o estado como EMERGENCY. O banco de dados está em modo de usuário único e pode ser reparado ou restaurado. O banco de dados está marcado como READ_ONLY, o log está desabilitado e o acesso é limitado aos membros da função de servidor fixa **sysadmin** . EMERGENCY é usado principalmente para a solução de problemas. Por exemplo, um banco de dados marcado como o suspeito pode ser definido como o estado EMERGENCY. Isso permitiria o acesso somente leitura do administrador de sistema ao banco de dados. Apenas membros da função de servidor fixa **sysadmin** podem definir um banco de dados com o estado EMERGENCY.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Estados de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [Estados de arquivo](../../relational-databases/databases/file-states.md)  
  
  
