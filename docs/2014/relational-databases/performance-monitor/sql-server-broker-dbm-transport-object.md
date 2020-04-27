---
title: Objeto de transporte SQL Server, Broker e DBM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0347c7f7e19ae5500f8c5be100ef2d0dc663784
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250725"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>Objeto SQL Server, Broker e DBM Transport
  O objeto de desempenho **Broker / DBM Transport** contém contadores de desempenho que relatam informações sobre o sistema de rede do Service Broker e do espelhamento de banco de dados. A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contador SQL Server Broker / DBM Transport|DESCRIÇÃO|  
|------------------------------------------------|-----------------|  
|**Bytes Atuais de E/S de Recebimento**|Esse contador informa o número de bytes a ser lido pelas operações de recebimento de transporte em execução.|  
|**Bytes Atuais de E/S de Envio**|Esse contador informa o número total de bytes de fragmentos de mensagens que estão no processo de envio pela rede.|  
|**Fragmentos de Mens. Atuais de E/S de Envio**|Esse contador informa o número total de fragmentos de mensagens que estão no processo de envio pela rede.|  
|**Envios de Fragmento de Mensagem P1/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 1 enviados pela rede por segundo.|  
|**Envios de Fragmento de Mensagem P2/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 2 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P3/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 3 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P4/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 4 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P5/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 5 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P6/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 6 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P7/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 7 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P8/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 8 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P9/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 9 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P10/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 10 enviados pela rede por segundo.|  
|**Tamanho Médio do Envio de Fragmento de Mensagem**|Esse contador informa o tamanho médio dos fragmentos de mensagem enviados pela rede.|  
|**Envios de Fragmentos de Mensagem/s**|Esse contador informa o número de fragmentos de mensagem de todas as prioridades enviados pela rede por segundo.|  
|**Recebimentos de Fragmento de Mensagem/s**|Esse contador informa o número de fragmentos de mensagem recebidos pela rede por segundo.|  
|**Tam. Méd. Receb. de Frag. de Mensagem**|Esse contador informa o tamanho médio dos fragmentos de mensagem recebidos pela rede.|  
|**Contagem de Conexão Aberta**|Esse contador informa o número de conexões de rede abertas no Service Broker.|  
|**Bytes Pend. de E/S de Recebimento**|Esse contador informa o número de bytes contidos nos fragmentos de mensagem que foram recebidos pela rede mas que ainda não foram colocados em fila nem descartados.|  
|**Bytes Pendentes de E/S de Envio**|Esse contador informa o número total de bytes em fragmentos de mensagens que estão prontos para serem enviados pela rede.|  
|**Frag. de Mens. Pend. de E/S de Envio**|Esse contador informa o número de fragmentos de mensagem que foram recebidos pela rede mas que ainda não foram colocados em fila nem descartados.|  
|**Fragmentos de Mens. Pend. de E/S de Envio**|Esse contador informa o número total de fragmentos de mensagens que estão prontos para serem enviados pela rede.|  
|**Total de Bytes de E/S de Recebimento**|Esse contador informa o número total de bytes recebidos pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Bytes de E/S de recebimento/s**|Esse contador informa o número total de bytes por segundo recebidos pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Tam. Médio de E/S de Recebimento**|Esse contador informa o número médio de bytes de uma operação de recebimento de transporte.|  
|**E/Ss de Recebimento/s**|Esse contador informa o número de operações de E/S de recebimento de transporte por segundo que a camada de transporte do Service Broker / DBM concluiu. Observe que uma operação de recebimento de transporte pode conter mais de um fragmento de mensagem.|  
|**Total de Bytes de E/S de Envio**|Esse contador informa o número total de bytes enviados pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Bytes de E/S de Envio/s**|Esse contador informa o número total de bytes por segundo enviados pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Tamanho Médio de E/S de Envio**|Esse contador informa o tamanho médio em bytes de cada operação de envio de transporte. Observe que uma operação de envio de transporte pode conter mais de um fragmento de mensagem.|  
|**E/S de Envio/s**|Esse contador informa o número de operações de E/S de envio de transporte por segundo que foram concluídas. Observe que uma operação de envio de transporte pode conter mais de um fragmento de mensagem.|  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_broker_forwarded_messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
