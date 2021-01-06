---
title: Identificar esperas associadas a grupos de disponibilidade
description: Identifique esperas associadas a Grupos de Disponibilidade AlwaysOn usando o T-SQL (Transact-SQL) e eventos estendidos.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: how-to
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
author: rothja
ms.author: jroth
ms.openlocfilehash: ae57df2dfb3aa43f22ebed392b9ac35fd46c5d33
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641396"
---
# <a name="identify-waits-associated-with-availability-groups"></a>Identificar esperas associadas a grupos de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ao solucionar problemas de latência de Grupos de Disponibilidade Always On, as estatísticas de espera podem ser monitoradas para acúmulo, usando os tipos de espera de disponibilidade específicos de grupos na DMV (exibição de gerenciamento dinâmico) [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
 Para obter informações gerais sobre como usar estatísticas de espera, veja [Espera e filas do SQL Server 2005](/previous-versions/sql/sql-server-2005/administrator/cc966413(v=technet.10)). Esse documento foi escrito para o SQL Server 2005, mas as informações podem ser aplicadas a versões mais recentes do SQL Server.  
  
## <a name="query-for-availability-groups-wait-types"></a>Consultar tipos de espera de grupos de disponibilidade  
 Use a consulta T-SQL abaixo para recuperar todas as estatísticas de espera com os tipos de espera de grupos de disponibilidade:  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 Para monitorar as estatísticas de espera, capturando eventos estendidos, use o seguinte comando T-SQL.  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 Você pode exibir o mapeamento de chave-valor do tipo de espera executando a seguinte consulta:  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>Próximas etapas  
 [Tipos de esperas](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
