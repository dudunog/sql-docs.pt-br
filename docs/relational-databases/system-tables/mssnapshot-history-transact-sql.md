---
description: MSsnapshot_history (Transact-SQL)
title: MSsnapshot_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1431788854f869eadd84f06ea2bb1885b95286f2
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092396"
---
# <a name="mssnapshot_history-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsnapshot_history** contém linhas de histórico para os agentes de instantâneo associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Snapshot Agent.|  
|**runstatus**|**int**|O status da execução:<br /><br /> **1** = iniciar.<br /><br /> **2** = com sucesso.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = tentar novamente.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**duration**|**int**|A duração, em segundos, da sessão de mensagem.|  
|**feitos**|**nvarchar(255)**|O texto de mensagem.|  
|**delivered_transactions**|**int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**int**|O número de comandos entregues por segundo.|  
|**delivery_rate**|**float(53)**|A média de comandos entregues por segundo.|  
|**error_id**|**int**|A ID do erro na tabela do sistema [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) .|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
