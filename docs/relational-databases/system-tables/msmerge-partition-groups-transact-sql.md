---
description: MSmerge_partition_groups (Transact-SQL)
title: MSmerge_partition_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: cawrites
ms.author: chadam
ms.openlocfilehash: 823e2a57cd6292be59fe9dca7bb805b8eaa47d49
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098630"
---
# <a name="msmerge_partition_groups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_partition_groups** armazena uma linha para cada partição computada em um determinado banco de dados. Além das colunas listadas, uma coluna é adicionada a essa tabela, para cada função usada em um filtro de linha com parâmetros. Por exemplo, uma coluna chamada **HOST_NAME_FN** será adicionada à tabela se um filtro usar a função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) . Uma linha é armazenada para cada conjunto exclusivo de valores de função, que sincronizaram com esse Publicador. Dois ou mais assinantes que se sincronizam com exatamente o mesmo valor para todas essas funções compartilharão a mesma linha nessa tabela e, portanto, todos compartilharão a mesma ID de partição. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|Coluna de identidade que fornece um número de ID exclusivo para a partição pré-computada.|  
|**publication_number**|**smallint**|O número de publicação, que é armazenado em **sysmergepublications**.|  
|**maxgen_whenadded**|**bigint**|A geração mais alta conhecida no Publicador no momento em que a linha é inserida nessa tabela.|  
|**using_partition_groups**|**bit**|Indica se a partição pertence a uma publicação que usa partição pré-computada e pode ser um destes valores:<br /><br /> **0** = a publicação não usa partições computadas.<br /><br /> **1** = a publicação usa partições de computação<br /><br /> Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).|  
|**HOST_NAME_FN**|**nvarchar(128)**|O valor fornecido ao usar filtros de linha com parâmetros para gerar partições. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
