---
description: logmarkhistory (Transact-SQL)
title: logmarkhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
author: cawrites
ms.author: chadam
ms.openlocfilehash: ab2f877b99fdc15cc4543741999c20a9a4924cda
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098670"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada transação marcada que foi confirmada. Essa tabela é armazenada no banco de dados **msdb** .  
  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Banco de dados local onde transação marcada ocorreu.|  
|**mark_name**|**nvarchar(128)**|Nome fornecido pelo usuário para a transação marcada.|  
|**descrição**|**nvarchar(255)**|Descrição fornecida pelo usuário da transação marcada. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário de banco de dados que executou transação marcada. Pode ser NULL.|  
|**LSN**|**numeric(25,0)**|Número de sequência do log do registro da transação onde a marca ocorreu.|  
|**mark_time**|**datetime**|Hora da confirmação da transação marcada (hora local).|  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
