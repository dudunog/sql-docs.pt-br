---
title: Monitorando a replicação com o Monitor do Sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 108954dd920c215a16385d7e07b4212102b50369
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85005667"
---
# <a name="monitoring-replication-with-system-monitor"></a>Monitorando a replicação com o monitor do sistema
  O Monitor do Sistema do Windows[!INCLUDE[msCoName](../../../includes/msconame-md.md)] permite o uso de gráficos e relatórios para medir a eficiência do seu computador, e a identificação e solução de possíveis problemas (como uso desbalanceado de recursos, hardware insuficiente ou design de programa inadequado), e o planejamento de requisitos adicionais de hardware. Para obter mais informações, veja [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 O Monitor do Sistema usa objetos e contadores de desempenho que fornecem informações sobre o desempenho de vários processos. É possível medir o desempenho de replicação por meio de contadores associados com os agentes de replicação:  
  
|Agente|Objeto de desempenho|Contador|Descrição|  
|-----------|------------------------|-------------|-----------------|  
|Todos os agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agentes de replicação|Executando|O número de agentes de replicação que estão sendo executados no momento.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo da replicação|Instantâneo: Cmds/s entregues|O número de comandos por segundo entregues ao Distribuidor.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo da replicação|Instantâneo: Trans/s entregues|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Logreader de replicação|Logreader: Cmds/s entregues|O número de comandos por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Logreader de replicação|Logreader: Trans/s entregues|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Logreader de replicação|Logreader: latência de entrega|O período de tempo atual, em milissegundos, passado desde quando as transações foram aplicadas no Publicador até sua entrega no Distribuidor.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: Cmds/s entregues|O número de comandos por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: Trans/s entregues|O número de transações por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: latência de entrega|O período de tempo atual, em milissegundos, passado desde quando as transações foram entregues ao Distribuidor até sua aplicação no Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem da replicação|Conflitos/s|O número de conflitos por segundo ocorridos durante o processo de mesclagem.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem da replicação|Alterações baixadas/s|O número de linhas por segundo replicadas do Publicador ao Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem da replicação|Alterações Carregadas/s|O número de linhas por segundo replicadas do Assinante ao Publicador.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitoramento &#40;Replicação&#41;](../monitoring-replication.md)  
  
  
