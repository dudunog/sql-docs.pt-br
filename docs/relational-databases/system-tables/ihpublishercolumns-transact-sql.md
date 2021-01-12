---
description: IHpublishercolumns (Transact-SQL)
title: IHpublishercolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: cawrites
ms.author: chadam
ms.openlocfilehash: 44704435eca9e065e7065f025b4c99accab7fa7f
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092462"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHpublishercolumns** representa os metadados armazenados no Publicador. Essa tabela contém uma linha para cada coluna replicada de Editores não SQL Server usando o Distribuidor atual. As informações de tipo de dados em **IHpublishercolumns** são específicas para o DBMS (sistema de gerenciamento de banco de dados) não SQL Server do qual os dados são publicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica uma coluna publicada.|  
|**table_id**|**int**|Identifica a tabela de origem do [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) ao qual a coluna pertence.|  
|**publisher_id**|**smallint**|Identifica o Editor não SQL Server do qual a coluna está sendo publicada.|  
|**name**|**sysname**|O nome da coluna publicada.|  
|**column_ordinal**|**int**|Identifica a coluna por ordem.|  
|**tipo**|**varchar(255)**|O tipo de dados de coluna da coluna de origem no Publicador.|  
|**length**|**bigint**|O comprimento da coluna de origem no Publicador.|  
|**prec**|**int**|A precisão da coluna de origem no Publicador.|  
|**scale**|**int**|A escala da coluna de origem no Publicador.|  
|**IsNullable**|**bit**|Indica se a coluna aceita valores nulos, em que **1** significa que valores nulos são aceitos.|  
|**iscaptured**|**bit**|Indica se um gatilho existe ou não na coluna, que pode existir mesmo se a coluna não for publicada em um artigo. Um valor de **1** significa que o gatilho existe na coluna.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [&#41;sysarticlecolumns &#40;Transact-SQL ](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
