---
description: MSpub_identity_range (Transact-SQL)
title: MSpub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
author: cawrites
ms.author: chadam
ms.openlocfilehash: 526620d1fe5ed7c00eed23b4433f3f7630205153
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098536"
---
# <a name="mspub_identity_range-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSpub_identity_range** fornece suporte ao gerenciamento de intervalo de identidade. Essa tabela é armazenada no banco de dados de assinatura e publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|A ID da tabela que tem a coluna de identidade administrada pela replicação.|  
|**range**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos à assinatura em um ajuste.|  
|**pub_range**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos à publicação em um ajuste.|  
|**current_pub_range**|**bigint**|O intervalo atual usado pela publicação. Ele pode ser diferente de *pub_range* se for exibido depois de ser alterado por **sp_changearticle** e antes do próximo ajuste de intervalo.|  
|**threshold**|**int**|Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Quando a porcentagem de valores especificados no *limite* é usada, o agente de distribuição cria um novo intervalo de identidade.|  
|**last_seed**|**bigint**|A associação mais baixa do intervalo atual.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
