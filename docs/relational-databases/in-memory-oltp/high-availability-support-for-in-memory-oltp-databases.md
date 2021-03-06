---
title: Alta disponibilidade – bancos de dados OLTP in-memory
description: Os Bancos de Dados do SQL Server que contêm tabelas com otimização de memória, com ou sem procedimentos armazenados compilados nativos, são totalmente compatíveis com Grupos de Disponibilidade Always On.
ms.custom: seo-dt-2019
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9b275387efa5cc44b012cccef82fb3284e594abb
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98170538"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Suporte de alta disponibilidade para bancos de dados OLTP na memória
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Os bancos de dados que contêm tabelas com otimização de memória, com ou sem procedimentos armazenados compilados nativos, são totalmente compatíveis com Grupos de Disponibilidade AlwaysOn.  Não há nenhuma diferença na configuração e no suporte de bancos de dados que contêm objetos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] em comparação aos que não têm.  

 As alterações nas tabelas com otimização de memória na réplica primária são aplicadas às tabelas na réplica secundária durante a fase refazer. Isso permite um failover rápido para a réplica secundária, pois os dados já estão na memória. As tabelas estão disponíveis para consultas de leitura em réplicas secundárias que foram configuradas para acesso de leitura.  

  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>Grupos de Disponibilidade AlwaysOn e bancos de dados OLTP in-memory  
 Configurar bancos de dados com componentes [!INCLUDE[hek_2](../../includes/hek-2-md.md)] fornece os seguintes benefícios:  
  
-   **Uma experiência totalmente integrada**   
    Você pode configurar seus bancos de dados que contêm tabelas com otimização de memória usando o mesmo assistente com o mesmo nível de suporte para réplicas secundárias síncronas e assíncronas. Além disso, o monitoramento de integridade é fornecido usando o já familiar painel do AlwaysOn no SQL Server Management Studio.  
  
-   **Tempo de Failover comparável**   
    As réplicas secundárias mantêm o estado na memória das tabelas duráveis com otimização de memória. No caso de failover automático ou forçado, o tempo de failover para o novo primário é comparável às tabelas baseadas em disco, já que nenhuma recuperação é necessária. As tabelas com otimização de memória criadas como SCHEMA_ONLY têm suporte nesta configuração. No entanto, as alterações para essas tabelas não são registradas, portanto, nenhum dado existirá nessas tabelas na réplica secundária.  
  
-   **Secundária Legível**   
    Você pode acessar e consultar tabelas com otimização de memória na réplica secundária, caso ela tenha sido configurada para acesso de leitura. No [!INCLUDE[ssSQL15](../../includes/sssql16-md.md)], o carimbo de data/hora de leitura na réplica secundária está em sincronização próxima com o carimbo de data/hora de leitura na réplica primária, o que significa que as alterações na réplica primária se tornarão rapidamente visíveis na secundária. Esse comportamento de sincronização próxima é diferente do OLTP In-Memory do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  

### <a name="considerations"></a>Considerações

- O SQL Server 2019 apresentou a fase refazer paralela para bancos de dados do grupo de disponibilidade com otimização de memória. No SQL Server 2016 e 2017, as tabelas baseadas em disco não usarão a fase refazer paralela se um banco de dados em um grupo de disponibilidade também tiver otimização de memória. 
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Instância de Clustering de Failover (FCI) e bancos de dados OLTP na memória  
 Para obter alta disponibilidade em uma configuração de armazenamento compartilhado, você pode configurar a instância do cluster de failover com bancos de dados usando tabelas com otimização de memória. Considere os seguintes fatores como parte da configuração de uma FCI:  
  
-   **Objetivo de tempo de recuperação**   
    O tempo de failover provavelmente será maior conforme as tabelas com otimização de memória precisem ser carregadas na memória antes que o banco de dados seja disponibilizado.  
  
-   **Tabelas SCHEMA_ONLY**   
    Lembre-se de que as tabelas SCHEMA_ONLY estarão vazias e sem linhas após o failover. Isso é projetado e definido pelo aplicativo. E é exatamente o mesmo comportamento de quando você reinicia um banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)] com uma ou mais tabelas SCHEMA_ONLY.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Suporte para replicação de transação em OLTP na memória  
 As tabelas que atuam como assinantes de replicação transacional, com exceção da replicação transacional ponto a ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória.  Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: Réplicas Secundárias Legíveis (Grupos de Disponibilidade Always On)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
