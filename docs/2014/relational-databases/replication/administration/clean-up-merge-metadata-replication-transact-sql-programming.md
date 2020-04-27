---
title: Limpar metadados de mesclagem (programação de Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 384b5cc158600848dbca6528a4c8c39250a23908
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62629169"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Limpar metadados de mesclagem (Programação Transact-SQL de replicação)
  Os metadados de replicação de mesclagem são limpados periodicamente pelo Agente de Mesclagem com base na configuração de retenção para a publicação. Isso acontece no Publicador e Assinante no [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)e nas tabelas do sistema [de MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) . Também é possível limpar programaticamente os dados nessas tabelas usando procedimentos armazenados de replicação.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Para limpar os metadados de mesclagem manualmente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql).  
  
2.  Adicional Observe o número de linhas removidas na etapa 1 [da MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)e [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql) tabelas do sistema, retornadas respectivamente **@num_genhistory_rows**nos **@num_contents_rows**parâmetros de **@num_tombstone_rows** saída, e.  
  
3.  Repita as etapas 1 e 2 no Assinante para limpar os metadados no banco de dados de assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Validade e desativação de assinatura](../subscription-expiration-and-deactivation.md)  
  
  
