---
title: Configurar um grupo de disponibilidade de escala de leitura (SQL Server em Linux)
description: Saiba mais sobre como configurar um AG (grupo de disponibilidade) Always On do SQL Server para cargas de trabalho de escala de leitura no Linux.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 01/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4c0057327466773d759752ad6760b2e736b84ebb
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115945"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>Configurar um grupo de disponibilidade do SQL Server para escala de leitura no Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

É possível configurar um AG (grupo de disponibilidade) Always On do SQL Server para cargas de trabalho de escala de leitura no Linux. Há dois tipos de arquiteturas para grupos de disponibilidade. Uma arquitetura para alta disponibilidade usa um gerenciador de clusters para fornecer uma melhor continuidade dos negócios. Essa arquitetura também pode incluir réplicas de escala de leitura. Para criar a arquitetura de alta disponibilidade, confira [Configurar o grupo de disponibilidade Always On do SQL Server para alta disponibilidade no Linux](sql-server-linux-availability-group-configure-ha.md). A outra arquitetura é compatível apenas com cargas de trabalho de escala de leitura. Este artigo explica como criar um grupo de disponibilidade sem um gerenciador de clusters para cargas de trabalho de leitura de escala. Essa arquitetura fornece apenas uma escala de leitura. Ela não oferece alta disponibilidade.

> [!NOTE]
> Um grupo de disponibilidade com `CLUSTER_TYPE = NONE` pode incluir réplicas hospedadas em diferentes plataformas de sistema operacional. Ele não é compatível com alta disponibilidade. 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Criar o grupo de disponibilidade

Crie o grupo de disponibilidade. Defina `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = MANUAL`. Os aplicativos cliente que executam cargas de trabalho de análise ou relatório podem se conectar aos bancos de dados secundários diretamente. Também é possível criar uma lista de roteamento somente leitura. As conexões com a réplica primária encaminham solicitações de conexão de leitura para cada uma das réplicas secundárias da lista de roteamento usando um mecanismo round robin.

O script Transact-SQL a seguir cria um grupo de disponibilidade chamado `ag1`. O script configura as réplicas do grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração fará o SQL Server criar automaticamente o banco de dados em cada servidor secundário após ele ser adicionado ao grupo de disponibilidade. Atualize o script a seguir para o seu ambiente. Substitua os valores `<node1>` e `<node2>` pelos nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` valor pela porta definida para o ponto de extremidade. Execute o script Transact-SQL a seguir na réplica primária do SQL Server:

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH ( 
            ENDPOINT_URL = N'tcp://<node2>:<5022>', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-ag"></a>Ingressar SQL Servers secundários no grupo de disponibilidade

O script Transact-SQL a seguir ingressa um servidor em um grupo de disponibilidade chamado `ag1`. Atualize o script para o seu ambiente. Em cada réplica secundária do SQL Server, execute o seguinte script Transact-SQL para ingressar o grupo de disponibilidade:

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Esse grupo de disponibilidade não é uma configuração de alta disponibilidade. Se precisar de alta disponibilidade, siga as instruções contidas em [Configurar um grupo de disponibilidade Always On para SQL Server em Linux](sql-server-linux-availability-group-configure-ha.md). Especificamente, crie o AG com `CLUSTER_TYPE=WSFC` (em Windows) ou com `CLUSTER_TYPE=EXTERNAL` (em Linux). Depois integre com um gerenciador de clusters usando o clustering de failover do Windows Server no Windows ou o Pacemaker no Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conectar-se a réplicas secundárias somente leitura

Há duas maneiras de se conectar a réplicas secundárias somente leitura. Os aplicativos podem conectar-se diretamente à instância do SQL Server que hospeda a réplica secundária e consulta os bancos de dados. Eles também podem usar roteamento somente leitura, que requer um ouvinte.

* [Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [Roteamento somente leitura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Próximas etapas

* [Configurar um grupo de disponibilidade distribuído](../database-engine/availability-groups/windows/distributed-availability-groups.md)
* [Saiba mais sobre grupos de disponibilidade](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
* [Executar um failover manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)