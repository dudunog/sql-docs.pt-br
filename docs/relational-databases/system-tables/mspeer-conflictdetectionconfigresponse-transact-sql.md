---
title: MSpeer_conflictdetectionconfigresponse (T-SQL)
description: Descreve o MSPeer_conflictdetectionconfigureresponse procedimento armazenado usado em replicação ponto a ponto para armazenar a resposta de cada nó a uma repergunta de configuração em toda a topologia.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: cawrites
ms.author: chadam
ms.openlocfilehash: 02c82643c290e3b751ced451dd7415004272a2b0
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98097368"
---
# <a name="mspeer_conflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Usado em replicação ponto a ponto para armazenar a resposta de cada nó para solicitação de configuração de toda a topologia. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica uma entrada de solicitação de configuração de conflito na tabela de [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) .|  
|peer_node|**sysname**|O nome do instância do servidor que gerou a resposta.|  
|peer_db|**sysname**|Banco de dados de assinatura no par que gerou a resposta.|  
|peer_version|**sysname**|Identifica o número da versão do Publicador.|  
|peer_db_version|**sysname**|Identifica o número da versão do banco de dados de nível.|  
|is_peer|**bit**|Indica se um nó é um Assinante somente leitura. Um valor de **0** indicou um assinante somente leitura.|  
|conflict_detection_enabled|**bit**|Indica se detecção de conflito está ativada para a topologia.|  
|originator_id|**varbinary(16)**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Período de tempo, em dias, que os metadados são armazenados em tabelas de conflitos.|  
|peer_subscriptions|**XML**|Informações sobre o nó que respondeu à solicitação.|  
|progress_phase|**nvarchar(32)**|Identifica a fase atual de processamento, usando um dos seguintes valores:<br /><br /> Iniciado<br /><br /> Versão de nível coletada<br /><br /> Status coletado|  
|modified_date|**datetime**|Data e hora em que uma fase foi concluída.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
