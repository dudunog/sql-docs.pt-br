---
title: MSrepl_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3a44dd898b4ec4afcf161e398072edfbc3f6f815
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820067"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSrepl_errors** contém linhas com agente de distribuição estendido e informações de agente de mesclagem falha. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do erro.|  
|**time**|**datetime**|A hora da ocorrência do erro.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|A ID de tipo de origem do erro.|  
|**source_name**|**nvarchar (100)**|O nome de origem do erro.|  
|**error_code**|**sysname**|O código do erro.|  
|**error_text**|**ntext**|A mensagem de erro.|  
|**xact_seqno**|**varbinary(16)**|O número de sequência do log de transações inicial do lote de execução com falha. Usado somente por Distribution Agents, esse é o número de sequência do log de transações da primeira transação do lote de execução com falha.|  
|**command_id**|**int**|A ID de comando do lote de execução com falha. Usado somente por Distribution Agents, essa é a ID de comando do primeiro comando do lote de execução com falha.|  
|**session_id**|**int**|A ID da sessão de agente na qual ocorreu o erro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
