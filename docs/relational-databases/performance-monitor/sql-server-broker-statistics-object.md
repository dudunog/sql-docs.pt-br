---
title: SQL Server, objeto Estatísticas de Agente | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho SQLServer:Broker Statistics, que contém contadores de desempenho que relatam informações sobre o Service Broker para o Mecanismo de Banco de Dados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8c422fb14069e2fe290d2719c08331aa10229894
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505852"
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server, objeto Broker Statistics
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto de desempenho SQLServer:Broker Statistics inclui contadores de desempenho que relatam informações gerais sobre o [!INCLUDE[ssSB](../../includes/sssb-md.md)] para uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. A seguinte tabela lista os contadores incluídos nesse objeto:  
  
|Contadores do SQL Server Broker Statistics|Descrição|  
|-------------------------------------------|-----------------|  
|**Total de Erros de Ativação**|O número de vezes que um procedimento armazenado de ativação do [!INCLUDE[ssSB](../../includes/sssb-md.md)] fechou com um erro.|  
|**Reversões de Transações do Agente**|O número de transações revertidas que continham instruções DML relacionadas ao [!INCLUDE[ssSB](../../includes/sssb-md.md)], como SEND e RECEIVE.|  
|**Total de Mensagens Corrompidas**|O número de mensagens corrompidas que foram recebidas pela instância.|  
|**Mensagens de Transmissão Removidas da Fila/s**|O número de mensagens que foram removidas da fila de transmissão do [!INCLUDE[ssSB](../../includes/sssb-md.md)] por segundo.|  
|**Contagem de eventos do timer de caixa de diálogo**|O número de timers ativos na camada de protocolo de caixa de diálogo. Esse número corresponde ao número de caixas de diálogo ativas.|  
|**Total de Mensagens Descartadas**|O número de mensagens que foram recebidas pela instância, mas não puderam ser entregues em uma fila.|  
|**Total de Mensagens Locais Enfileiradas**|O número de mensagens que foram enfileiradas na instância, contando apenas aquelas que não chegaram pela rede.|  
|**Mensagens Locais Enfileiradas/s**|O número de mensagens que foram enfileiradas na instância por segundo, contando apenas aquelas que não chegaram pela rede.|  
|**Total de Mensagens Enfileiradas**|O número total de mensagens que foram enfileiradas na instância.|  
|**Mensagens Enfileiradas/s**|O número de mensagens que foram enfileiradas na instância por segundo. Inclui mensagens de todos os níveis de prioridade.|  
|**Mensagens P1 Enfileiradas/s**|O número de mensagens de prioridade 1 que foram enfileiradas na instância por segundo.|  
|**Mensagens P2 Enfileiradas/s**|O número de mensagens de prioridade 2 que foram enfileiradas na instância por segundo.|  
|**Mensagens P3 Enfileiradas/s**|O número de mensagens de prioridade 3 que foram enfileiradas na instância por segundo.|  
|**Mensagens P4 Enfileiradas/s**|O número de mensagens de prioridade 4 que foram enfileiradas na instância por segundo.|  
|**Mensagens P5 Enfileiradas/s**|O número de mensagens de prioridade 5 que foram enfileiradas na instância por segundo.|  
|**Mensagens P6 Enfileiradas/s**|O número de mensagens de prioridade 6 que foram enfileiradas na instância por segundo.|  
|**Mensagens P7 Enfileiradas/s**|O número de mensagens de prioridade 7 que foram enfileiradas na instância por segundo.|  
|**Mensagens P8 Enfileiradas/s**|O número de mensagens de prioridade 8 que foram enfileiradas na instância por segundo.|  
|**Mensagens P9 Enfileiradas/s**|O número de mensagens de prioridade 9 que foram enfileiradas na instância por segundo.|  
|**Mensagens P10 Enfileiradas/s**|O número de mensagens de prioridade 10 que foram enfileiradas na instância por segundo.|  
|**Mensagens de Transmissão Enfileiradas/s**|O número de mensagens que foram colocadas na fila de transmissão do [!INCLUDE[ssSB](../../includes/sssb-md.md)] por segundo.|  
|**Total de Frag. de Mens. de Transp. Enfileirados**|O número de fragmentos de mensagens que foram enfileirados na instância, contando apenas aqueles que chegaram pela rede.|  
|**Fragmentos de Mensagens de Transporte Enfileirados/s**|O número de fragmentos de mensagens que foram enfileirados na instância por segundo.|  
|**Total de Mensagens de Transporte Enfileiradas**|O número de mensagens que foram enfileiradas na instância, contando apenas aquelas que chegaram pela rede.|  
|**Mensagens de Transporte Enfileiradas/s**|O número de mensagens que foram enfileiradas na instância por segundo, contando apenas aquelas que chegaram pela rede.|  
|**Total de Mensagens Encaminhadas**|O número total de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] encaminhadas por este computador.|  
|**Mensagens Encaminhadas/s**|O número de mensagens por segundo encaminhadas por este computador.|  
|**Total de Bytes de Mensagens Encaminhadas**|O tamanho total, em bytes, das mensagens encaminhas por este computador.|  
|**Bytes de Mensagens Encaminhadas/s**|O tamanho, em bytes, das mensagens encaminhas por este computador por segundo.|  
|**Total de Mensagens Encaminhadas Descartadas**|O número de mensagens que este computador recebeu para encaminhar, mas não encaminhou com êxito.|  
|**Mensagens Encaminhadas Descartadas/s**|O número de mensagens por segundo que este computador recebeu para encaminhar, mas não encaminhou com êxito.|  
|**Bytes de Mensagens Pendentes Encaminhadas**|O tamanho total das mensagens que estão retidas para serem encaminhadas.|  
|**Contagem de Mensagens Pendentes Encaminhadas**|O número total de mensagens que estão retidas para serem encaminhadas.|  
|**RECEIVE Total do SQL**|O número total de instruções RECEIVE [!INCLUDE[tsql](../../includes/tsql-md.md)] processadas.|  
|**RECEIVEs do SQL/s**|O número de instruções RECEIVE [!INCLUDE[tsql](../../includes/tsql-md.md)] processadas por segundo.|  
|**SEND Total do SQL**|O número total de instruções SEND [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas.|  
|**SENDs do SQL/s**|O número de instruções SEND [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
