---
title: MSSQL_ENG014165 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014165 error
ms.assetid: 7bb07672-310c-4f51-ae76-c55e7c8d51ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 77792826a80a4564e5f0fd7be2904d99029c3fe7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62864907"
---
# <a name="mssql_eng014165"></a>MSSQL_ENG014165
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14165|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o agente de mesclagem está sendo executado e pode atender ao requisito esperado.|  
  
## <a name="explanation"></a>Explicação  
 A replicação permite habilitar avisos para várias condições. Isso inclui falha ao processar um número suficiente de linhas quando a sincronização faz alterações entre uma fusão de Publicador e Assinante. É possível especificar horários diferentes para conexões discadas e LAN.  
  
 Ao habilitar um aviso usando o Replication Monitor ou o [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql), você especifica um limite que determina quando um aviso é disparado. Quando esse limite é atingido ou excedido, um aviso é exibido no Replication Monitor e um evento é gravado no log de eventos do Windows. Ao atingir um limite, também é possível disparar um alerta do SQL Server Agent. Para obter mais informações, consulte [Definir limites e avisos no Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Monitorar a replicação de forma programática](monitoring-replication.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Se uma assinatura não alcançar o limite de processamento de uma linha, será necessário determinar se há um problema de desempenho no sistema ou se o limite deve ser ajustado. Após configurar a replicação, desenvolva uma linha de base de desempenho, a qual permitirá determinar como a replicação se comporta com uma carga de trabalho típica para seus aplicativos e topologia. Inclua o número de linhas processadas nessa linha de base de forma que seja possível definir um valor apropriado para o limite.  
  
 Se o valor do limite for apropriado, mas estiver sendo excedido, será necessário determinar se há algum gargalo no desempenho do sistema. Para obter mais informações sobre como monitorar e solucionar problemas relacionados a desempenho de replicação, consulte os seguintes tópicos:  
  
-   [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md) (especialmente, a seção “Exibindo o desempenho de sincronização detalhado para replicação de mesclagem”)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
