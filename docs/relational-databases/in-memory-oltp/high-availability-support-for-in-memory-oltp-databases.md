---
title: Alta disponibilidade – bancos de dados OLTP in-memory
ms.custom: seo-dt-2019
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd467c8f6d942f53dade5ec6bb7d46ae9f39bdd9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412673"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Suporte de alta disponibilidade para bancos de dados OLTP na memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os bancos de dados que contêm tabelas com otimização de memória, com ou sem procedimentos armazenados compilados nativos, são totalmente compatíveis com Grupos de Disponibilidade AlwaysOn.  Não há nenhuma diferença na configuração e no suporte para bancos de dados que contêm objetos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] em comparação a aqueles sem.  
  
 Quando um banco de dados OLTP in-memory for implantado em uma configuração de Grupo de Disponibilidade AlwaysOn, as alterações nas tabelas com otimização de memória na réplica primária serão aplicadas à memória para as tabelas nas réplicas secundárias, quando REDO for aplicado. Isso significa que o failover para uma réplica secundária pode ser muito rápido, pois os dados já estão na memória. Além disso, as tabelas estão disponíveis para consultas em réplicas secundárias que foram configuradas para acesso de leitura.  
  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>Grupos de Disponibilidade AlwaysOn e bancos de dados OLTP in-memory  
 Configurar bancos de dados com componentes [!INCLUDE[hek_2](../../includes/hek-2-md.md)] fornece o seguinte:  
  
-   **Uma experiência totalmente integrada**   
    Você pode configurar seus bancos de dados que contêm tabelas com otimização de memória usando o mesmo assistente com o mesmo nível de suporte para réplicas secundárias síncronas e assíncronas. Além disso, o monitoramento de integridade é fornecido usando o já familiar painel do AlwaysOn no SQL Server Management Studio.  
  
-   **Tempo de Failover comparável**   
    As réplicas secundárias mantêm o estado na memória das tabelas duráveis com otimização de memória. No caso de failover automático ou forçado, o tempo de failover para o novo primário é comparável a tabelas de bases de disco, já que nenhuma recuperação é necessária. As tabelas com otimização de memória criadas como SCHEMA_ONLY têm suporte nesta configuração. No entanto, as alterações para essas tabelas não são registradas e, portanto, nenhum dado existirá nessas tabelas na réplica secundária.  
  
-   **Secundária Legível**   
    Você pode acessar e consultar tabelas com otimização de memória na réplica secundária se ela tiver sido configurada para acesso de leitura. No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o carimbo de data/hora de leitura na réplica secundária está em sincronização próxima com o carimbo de data/hora de leitura na réplica primária, o que significa que as alterações na réplica primária se tornarão visíveis na secundária muito rapidamente. Esse comportamento de sincronização próxima é diferente do OLTP in-memory do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Instância de Clustering de Failover (FCI) e bancos de dados OLTP na memória  
 Para obter alta disponibilidade em uma configuração de armazenamento compartilhado, você pode configurar o clustering de failover nas instâncias com um ou mais bancos de dados com tabelas com otimização de memória. Você precisa considerar os seguintes fatores como parte da configuração de uma FCI.  
  
-   **Objetivo de tempo de recuperação**   
    O tempo de failover provavelmente será maior conforme as tabelas com otimização de memória devam ser carregadas na memória antes que o banco de dados seja disponibilizado.  
  
-   **Tabelas SCHEMA_ONLY**   
    Lembre-se de que as tabelas SCHEMA_ONLY estarão vazias e sem linhas após o failover. Isso é projetado e definido pelo aplicativo. E é exatamente o mesmo comportamento de quando você reinicia um banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)] com uma ou mais tabelas SCHEMA_ONLY.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Suporte para replicação de transação em OLTP na memória  
 As tabelas que atuam como assinantes de replicação transacional, com exceção da replicação transacional ponto a ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória.  Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: réplicas secundárias legíveis (Grupos de Disponibilidade AlwaysOn)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
