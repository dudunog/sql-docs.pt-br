---
description: MSsubscription_articles (Transact-SQL)
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: cawrites
ms.author: chadam
ms.openlocfilehash: c8ae84063723c76745776a4e530f7fb8d63b008a
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098502"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsubscription_articles** contém informações sobre os artigos em uma assinatura enfileirada. Essa tabela só é populada para tipos de replicação de atualização enfileirada e atualização imediata com atualização enfileirada como um failover.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do agente que serve a este artigo|  
|**artid**|**int**|A ID do artigo da tabela **sysarticles** .|  
|**artigo**|**sysname**|O nome do artigo da tabela **sysarticles** .|  
|**dest_table**|**sysname**|O nome da tabela de destino da tabela **sysarticles** .|  
|**proprietário**|**sysname**|O proprietário da assinatura.|  
|**cft_table**|**sysname**|O nome da tabela de conflito para este artigo, para tipo de replicação de atualização enfileirada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
