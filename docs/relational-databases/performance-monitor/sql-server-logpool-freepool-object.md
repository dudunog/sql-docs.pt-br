---
title: SQL Server, objeto LogPool FreePool | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:LogPool FreePool
ms.assetid: 8ffd569b-045f-4c3f-a473-4a491d6a1d80
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c51fb2a86cb33facfa7b54fe35deb6efe9cdef71
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775837"
---
# <a name="sql-server-logpool-freepool-object"></a>SQL Server, objeto LogPool FreePool
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O objeto de desempenho **SQLServer:LogPool FreePool** fornece contadores de estatísticas para o pool livre dentro do Pool de Logs.

A tabela a seguir descreve os objetos de desempenho **LogPool FreePool** do SQL Server.

|**Contadores de LogPool FreePool do SQL Server**|DESCRIÇÃO|  
|-------------|-----------------|  
|**Reabastecimentos do Buffer Gratuito/seg**|Número de buffers alocados para reabastecimento por segundo.|
|**Comprimento de lista livre**|Comprimento da lista livre.|

Há uma instância do contador para cada categoria do pool de logs.

## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)

