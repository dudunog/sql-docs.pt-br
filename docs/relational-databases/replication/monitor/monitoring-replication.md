---
title: Monitoramento (replicação) | Microsoft Docs
description: Saiba mais sobre as ferramentas de monitoramento usadas para acompanhar a atividade e o status da replicação na topologia de Replicação do SQL Server.
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: fb514bd2a96e797a6ed0e2cdd275dd397762fe90
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918655"
---
# <a name="monitoring-replication"></a>Monitorando (Replicação)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Monitorar uma topologia de replicação é um aspecto importante na implantação da replicação. Já que a atividade de replicação é distribuída, é essencial controlar sua atividade e o status em todos os computadores envolvidos na replicação. Com o uso de várias ferramentas de monitoramento, você pode responder perguntas comuns como: 

-   Meu sistema de replicação está íntegro?
-   Quais assinaturas estão lentas?
-   A minha assinatura transacional está muito atrás na fila?
-   Quanto tempo uma transação confirmada agora, levará para alcançar um Assinante em replicação transacional?
-   Por que minha assinatura de mesclagem está lenta?
-   Por que um agente não está executando?  
  

As seguintes ferramentas podem ser usadas para monitorar a replicação:  
  
-   **Monitor de Replicação do SQL Server** – a ferramenta mais importante para monitorar a replicação, apresentando uma exibição do Editor dedicada a toda atividade de replicação. Para obter mais informações, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md). 
-   **SQL Server Management Studio** – fornece acesso ao Replication Monitor. Também permite que você exiba o status atual e a última mensagem registrada pelos seguintes agentes e permite que você inicie e interrompa cada agente: Agente de Leitor de Log, Agente de Instantâneo, Agente de Mesclagem e Agente de Distribuição. Para obter mais informações, consulte [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   **Transact-SQL (T-SQL) e RMO (Replication Management Objects)** – ambas as interfaces permitem que você monitore todos os tipos de replicação do distribuidor. A replicação de mesclagem fornece também a capacidade de monitorar a replicação a partir do Assinante.  
  
-   **Alertas para eventos do agente de replicação** – A replicação fornece vários alertas predefinidos para os eventos do agente de replicação e você pode criar alertas adicionais se necessário. Os alertas podem ser usados para acionar uma resposta automatizada a um evento e/ou notificar um administrador. Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   **Monitor do Sistema** – pode ser útil para monitorar o desempenho, ao fornecer vários contadores para a replicação. Para obter mais informações, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  

## <a name="see-also"></a>Consulte Também  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
