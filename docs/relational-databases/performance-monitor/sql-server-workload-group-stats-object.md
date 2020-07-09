---
title: SQL Server, objeto Estatísticas de grupo de cargas de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 1413ab35860b20a80e1fcae07a0aa5534c1e3965
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758885"
---
# <a name="sql-server-workload-group-stats-object"></a>SQL Server, objeto de estatísticas de grupo de cargas de trabalho
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto SQLServer:Estatísticas de Grupo de Cargas de Trabalho contém contadores de desempenho que dão informações sobre estatísticas de grupo de cargas de trabalho do Administrador de Recursos.  
  
 Cada grupo de cargas de trabalho ativo cria uma instância do objeto de desempenho SQLServer:Estatísticas de Grupo de Cargas de Trabalho que tem o mesmo nome de instância do grupo de cargas de trabalho do Administrador de Recursos. A tabela a seguir descreve os contadores suportados nesta instância.  
  
|Nome do contador|DESCRIÇÃO|  
|------------------|-----------------|  
|**Threads paralelos ativos**|A contagem atual de uso de threads paralelos.|  
|**Solicitações ativas**|O número de solicitações que estão sendo executadas neste grupo de cargas de trabalho. Deverá ser equivalente à contagem de linhas de sys.dm_exec_requests filtradas pela ID de grupo.|  
|**Solicitações bloqueadas**|O número atual de solicitações bloqueadas no grupo de cargas de trabalho. Esse número pode ser usado para determinar características de carga de trabalho.|  
|**% de CPU atrasada**|CPU do sistema atrasada para todas as solicitações na instância especificada do objeto de desempenho como uma porcentagem do tempo total ativo.| 
|**% base de CPU atrasada**|Apenas para uso interno.| 
|**% de CPU efetiva**|Uso de CPU do sistema por todas as solicitações na instância especificada do objeto de desempenho como uma porcentagem do tempo total ativo.| 
|**% base de CPU efetiva**|Apenas para uso interno.| 
|**% de uso de CPU**|O uso da largura de banda da CPU por todas as solicitações neste grupo de cargas de trabalho calculado em relação ao computador e normalizado para todas as CPUs do sistema. Esse valor mudará à medida que a quantidade de CPU disponível para o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for alterada. Ele não é normalizado de acordo com o que é recebido pelo processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .| 
|**% base de uso de CPU**|Apenas para uso interno.| 
|**% de CPU violada**|A diferença entre a reserva de CPU e a porcentagem de agendamento efetiva.|  
|**Tempo máximo de CPU da solicitação (ms)**|O tempo máximo de CPU, em milissegundos, usado por uma solicitação que está sendo executada no grupo de cargas de trabalho.|  
|**Concessão máxima de memória da solicitação (KB)**|O valor máximo da concessão de memória, em kilobytes (KB), para uma consulta.|  
|**Otimizações de consultas/seg**|O número de otimizações de consulta por segundo ocorridas neste grupo de cargas de trabalho. Esse número pode ser usado para determinar características de carga de trabalho.|  
|**Solicitações em fila**|O número atual de solicitações em fila que estão esperando para serem selecionadas. Esta contagem poderá ser diferente de zero se a aceleração ocorrer depois que o limite GROUP_MAX_REQUESTS for atingido.|  
|**Concessões de memória reduzidas/s**|O número de consultas que estão obtendo menos do que a quantidade ideal de concessões de memória por segundo.|  
|**Solicitações concluídas/s**|O número de solicitações que foram concluídas neste grupo de cargas de trabalho. Este número é cumulativo.|  
|**Planos de qualidade inferior/s**|O número de planos de qualidade inferior que são gerados por segundo neste grupo de cargas de trabalho.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto de estatísticas do pool de recursos](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
