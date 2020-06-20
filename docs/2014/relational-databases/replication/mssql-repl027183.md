---
title: MSSQL_REPL027183 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 712d7a93dbd2328de031001d9f5ab12e7e4732da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060674"
---
# <a name="mssql_repl027183"></a>MSSQL_REPL027183
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|27183|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo de mesclagem não pôde enumerar as alterações nos artigos que apresentaram filtros de linha com parâmetros. Se a falha persistir, aumente o tempo limite da consulta nesse processo, reduza o período de retenção da publicação e aprimore os índices nas tabelas publicadas.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro surge quando o tempo limite do Merge Agent ocorre durante o processamento de alterações em uma publicação filtrada. O tempo limite pode ser causado por um dos seguintes problemas:  
  
-   A otimização das partições pré-computadas não está sendo usada.  
  
-   Fragmentação de índice em colunas usadas para filtragem.  
  
-   Tabelas de metadados de mesclagens grandes, como **MSmerge_tombstone**, **MSmerge_contents**e **MSmerge_genhistory**.  
  
-   Tabelas filtradas não associadas em uma chave exclusiva e associação de filtros que envolvem um grande número de tabelas.  
  
## <a name="user-action"></a>Ação do usuário  
 Como resolver o problema:  
  
-   Aumente o valor do parâmetro **-QueryTimeOut** do Agente de Mesclagem para permitir que o processamento continue enquanto você aborda os problemas subjacentes que estão provocando o erro. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](agents/replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md).  
  
-   Use a otimização de partições pré-computadas, se possível. Por padrão, essa otimização será usada se um número de requisitos de publicação forem atendidos. Para obter mais informações sobre esses requisitos, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](merge/parameterized-filters-optimize-for-precomputed-partitions.md). Se a publicação não satisfizer esses requisitos, considere reprojetar a publicação.  
  
-   Especifique a menor definição possível para o período de retenção da publicação, porque a replicação não poderá limpar os metadados nos bancos de dados de assinatura e publicação antes do período de retenção ser atingido. Para obter mais informações, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
-   Como parte da manutenção da replicação de mesclagem, verifique esporadicamente o crescimento das tabelas do sistema associadas à replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, veja [Reorganizar e recriar índices](../indexes/indexes.md).  
  
-   Certifique-se de que as colunas usadas para filtragem estejam indexadas corretamente e reconstrua tais índices, se necessário. Para obter mais informações, veja [Reorganizar e recriar índices](../indexes/indexes.md).  
  
-   Defina a propriedade **join_unique_key** para filtros de junção com base em colunas exclusivas. Para obter mais informações, consulte [Join Filters](merge/join-filters.md).  
  
-   Limite o número de tabelas na hierarquia de filtro de junção. Se você estiver gerando filtros de junção de cinco ou mais tabelas, considere outras soluções: não filtre tabelas pequenas, que não estão sujeitas a alterações ou que sejam basicamente tabelas de pesquisa. Use filtros de junção somente entre tabelas que devem ser particionadas entre assinaturas.  
  
-   Faça um número menor de alterações em tabelas filtradas entre as sincronizações ou execute o Merge Agent mais frequentemente. Para obter mais informações sobre como definir agendas de sincronização, consulte [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
