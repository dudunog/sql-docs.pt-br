---
description: sys.dm_exec_compute_pools (Transact-SQL)
title: sys.dm_exec_compute_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=sql-server-ver15||>=sql-server-linux-2017'
ms.openlocfilehash: a55148fe8cc50e2237320ba5646cfbd55fff3365
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101582"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys.dm_exec_compute_pools (Transact-SQL)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome do pool de computação. Não permite valor nulo. Retorna `default` para o pool de computação padrão. |
|compute_pool_id|`int`|Identificador exclusivo do pool. Chave para esta exibição.|  
|local|`sysname`|Ponto de extremidade para controlador em um cluster de Big data do SQL. Não permite valor nulo. |

## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.

## <a name="see-also"></a>Consulte Também

[O que [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] são ](../../big-data-cluster/big-data-cluster-overview.md)?
