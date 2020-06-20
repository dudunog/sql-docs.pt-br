---
title: Suporte de alta disponibilidade para bancos de dados OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b0214b2ec0fbc712873d4c39732425a78ef31653
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050191"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Suporte de alta disponibilidade para bancos de dados OLTP na memória
  Os bancos de dados que contêm tabelas com otimização de memória, com ou sem procedimentos armazenados compilados nativos, são totalmente compatíveis com Grupos de Disponibilidade AlwaysOn.  Não nenhuma diferença na configuração e no suporte para bancos de dados que contenham objetos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] em comparação com aqueles sem,  
  
## <a name="alwayson-availability-groups-and-in-memory-oltp-databases"></a>Grupos de Disponibilidade AlwaysOn e bancos de dados OLTP na memória  
 Configurar bancos de dados com componentes [!INCLUDE[hek_2](../../includes/hek-2-md.md)] fornece o seguinte:  
  
-   **Uma experiência totalmente integrada**   
    Você pode configurar seus bancos de dados que contêm tabelas com otimização de memória usando o mesmo assistente com o mesmo nível de suporte para réplicas secundárias síncronas e assíncronas. Além disso, o monitoramento de integridade é fornecido usando o já familiar painel do AlwaysOn no SQL Server Management Studio.  
  
-   **Tempo de failover comparável**   
    As réplicas secundárias mantêm o estado na memória das tabelas duráveis com otimização de memória. No caso de failover automático ou forçado, o tempo de failover para o novo primário é comparável a tabelas de bases de disco, já que nenhuma recuperação é necessária. As tabelas com otimização de memória criadas como SCHEMA_ONLY têm suporte nesta configuração. No entanto, as alterações para essas tabelas não são registradas e, portanto, nenhum dado existirá nessas tabelas na réplica secundária.  
  
-   **Secundário legível**   
    Você pode acessar e consultar tabelas com otimização de memória na réplica secundária se ela tiver sido configurada para acesso de leitura. Para obter mais informações, consulte [Secundárias ativas: réplicas secundárias legíveis (Grupos de Disponibilidade AlwaysOn)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Instância de Clustering de Failover (FCI) e bancos de dados OLTP na memória  
 Para obter alta disponibilidade em uma configuração de armazenamento compartilhado, você pode configurar o clustering de failover nas instâncias com um ou mais bancos de dados com tabelas com otimização de memória. Você precisa considerar os seguintes fatores como parte da configuração de uma FCI.  
  
-   **Objetivo de tempo de recuperação**   
    O tempo de failover provavelmente será maior conforme as tabelas com otimização de memória devam ser carregadas na memória antes que o banco de dados seja disponibilizado.  
  
-   **SCHEMA_ONLY tabelas**   
    Lembre-se de que as tabelas SCHEMA_ONLY estarão vazias e sem linhas após o failover. Isso é projetado e definido pelo aplicativo. E é exatamente o mesmo comportamento de quando você reinicia um banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)] com uma ou mais tabelas SCHEMA_ONLY.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Suporte para replicação de transação em OLTP na memória  
 As tabelas que atuam como assinantes de replicação transacional, com exceção da replicação transacional ponto a ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória.  Para obter mais informações, consulte [replicação para assinantes de tabela com otimização de memória](../replication/replication-to-memory-optimized-table-subscribers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replicação para assinantes de tabela com otimização de memória](../replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
