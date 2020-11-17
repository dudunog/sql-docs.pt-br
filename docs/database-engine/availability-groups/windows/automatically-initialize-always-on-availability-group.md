---
title: Inicializar um grupo de disponibilidade usando propagação automática
description: Use a propagação automática para criar automaticamente réplicas secundárias para cada banco de dados em um grupo de disponibilidade Always On sem precisar fazer backup e restauração manuais.
ms.custom: seo-lt-2019
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: 67c6a601-677a-402b-b3d1-8c65494e9e96
author: cawrites
ms.author: chadam
ms.openlocfilehash: 81724be8012eea9aa1c6fcefbb7becc4a96092bf
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584707"
---
# <a name="use-automatic-seeding-to-initialize-an-always-on-availability-group"></a>Usar a propagação automática para inicializar um Grupo de Disponibilidade AlwaysOn
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

O SQL Server 2016 introduz a propagação automática de grupos de disponibilidade. Quando você cria um grupo de disponibilidade com propagação automática, o SQL Server cria automaticamente as réplicas secundárias para cada banco de dados no grupo. Não é mais necessário fazer backup e restaurar manualmente as réplicas secundárias. Para habilitar a propagação automática, crie o grupo de disponibilidade com o T-SQL ou use a versão mais recente do SQL Server Management Studio.

Para obter mais informações de histórico, consulte [Propagação automática para réplicas secundárias](automatic-seeding-secondary-replicas.md).
 
## <a name="prerequisites"></a>Prerequisites

No SQL Server 2016, a propagação automática exige que os dados e o caminho do arquivo de log sejam os mesmos em cada instância do SQL Server que participa do grupo de disponibilidade. No SQL Server 2017, você pode usar caminhos diferentes, porém a Microsoft recomenda usar os mesmos caminhos quando todas as réplicas estão hospedadas na mesma plataforma (por exemplo Windows ou Linux). Os grupos de disponibilidade da plataforma cruzada têm caminhos diferentes para as réplicas. Para obter detalhes, consulte [Layout de disco](automatic-seeding-secondary-replicas.md#disklayout).

A propagação do grupo de disponibilidade se comunica por meio do ponto de extremidade do espelhamento de banco de dados. Abra as regras de firewall de entrada para a porta do ponto de extremidade de espelhamento em cada servidor.

Os bancos de dados em um grupo de disponibilidade devem estar no modelo de recuperação completa. O banco de dados precisa ter um backup completo atual e o backup do log de transações. Esses arquivos de backup não são usados para a propagação automática, mas são necessários antes da inclusão do banco de dados em um grupo de disponibilidade. 
 
## <a name="create-availability-group-with-automatic-seeding"></a>Criar um grupo de disponibilidade com a propagação automática

Para criar um grupo de disponibilidade com propagação automática, defina `SEEDING_MODE=AUTOMATIC`. 

O exemplo a seguir cria um grupo de disponibilidade em um cluster de failover do Windows Server de dois nós. Antes de executar os scripts, atualize os valores de seu ambiente.

1. Crie os pontos de extremidade. Cada servidor precisa de um ponto de extremidade. O script a seguir cria um ponto de extremidade que usa a porta TCP 5022 para o ouvinte. Defina `<endpoint_name>` e `LISTENER_PORT` para que correspondam ao seu ambiente e execute o script em ambos os servidores:

    ```sql
    CREATE ENDPOINT [<endpoint_name>] 
        STATE=STARTED
        AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
        FOR DATA_MIRRORING (
            ROLE = ALL, 
            AUTHENTICATION = WINDOWS NEGOTIATE, 
            ENCRYPTION = REQUIRED ALGORITHM AES
            )
    GO
    ```

1. Crie o grupo de disponibilidade. O script a seguir cria o grupo de disponibilidade. Atualize os valores entre colchetes angulares `<>` para o nome do grupo, os nomes de servidor e os nomes de domínio e execute-os na instância primária do SQL Server.  

    ```sql
    CREATE AVAILABILITY GROUP [<availability_group_name>]
        FOR DATABASE db1
        REPLICA ON'<*primary_server*>'
        WITH (ENDPOINT_URL = N'TCP://<primary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC),
        N'<secondary_server>' WITH (ENDPOINT_URL = N'TCP://<secondary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC);
    GO
    ``` 

1. Ingresse na instância de servidor secundária no grupo de disponibilidade e conceda permissão para criar bancos de dados ao grupo de disponibilidade. Atualize o script a seguir, substitua os valores entre colchetes angulares `<>` para seu ambiente e execute-o na instância de réplica secundária do SQL Server: 
 
    ```sql
    ALTER AVAILABILITY GROUP [<availability_group_name>] JOIN
    GO  
    ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
    GO
    ```

O SQL Server cria automaticamente a réplica do banco de dados no servidor secundário. Se o banco de dados for grande, poderá levar algum tempo até a conclusão da sincronização do banco de dados. Se um banco de dados estiver em um grupo de disponibilidade configurado para a propagação automática, você poderá consultar a exibição do sistema `sys.dm_hadr_automatic_seeding` para monitorar o progresso da propagação. A consulta a seguir retorna uma linha para cada banco de dados que está em um grupo de disponibilidade configurado para a propagação automática.

```sql 
SELECT start_time,
    ag.name,
    db.database_name,
    current_state,
    performed_seeding,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding autos 
    JOIN sys.availability_databases_cluster db 
        ON autos.ag_db_id = db.group_database_id
    JOIN sys.availability_groups ag 
        ON autos.ag_id = ag.group_id
```

## <a name="prevent-automatic-seeding-after-an-availability-group"></a>Impedir a propagação automática após um grupo de disponibilidade

Para impedir temporariamente a réplica primária de propagar mais bancos de dados na réplica secundária, é possível negar a permissão do grupo de disponibilidade para criar bancos de dados. Execute a consulta a seguir na instância que hospeda a réplica secundária para negar a permissão do grupo de disponibilidade para criar bancos de dados de réplica.

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    DENY CREATE ANY DATABASE
GO
```


## <a name="enable-automatic-seeding-on-an-existing-availability-group"></a>Habilitar a propagação automática em um grupo de disponibilidade existente

É possível definir a propagação automática em um banco de dados existente. O comando a seguir altera um grupo de disponibilidade para usar a propagação automática. Execute o seguinte comando na réplica primária.

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>' 
    WITH (SEEDING_MODE = AUTOMATIC)
GO
```

O comando anterior força um banco de dados a reiniciar a propagação, se necessário. Por exemplo, se a propagação falhar devido a espaço em disco insuficiente na réplica secundária, execute `ALTER AVAILABILITY GROUP ... WITH (SEEDING_MODE=AUTOMATIC)` para reiniciar a propagação depois de adicionar espaço livre.

## <a name="stop-automatic-seeding"></a>Interromper a propagação automática

Para interromper a propagação automática de um grupo de disponibilidade, execute o seguinte script na réplica primária:

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>'   
    WITH (SEEDING_MODE = MANUAL)
GO
```

O script anterior cancela todas as réplicas que estão sendo propagadas atualmente e impede que o SQL Server inicialize automaticamente as réplicas neste grupo de disponibilidade. Isso não interrompe a sincronização das réplicas que já foram inicializadas. 


## <a name="monitor-automatic-seeding-availability-group"></a>Monitorar o grupo de disponibilidade com propagação automática

### <a name="use-system-dynamic-management-views-to-monitor-seeding"></a>Usar as exibições de gerenciamento dinâmico do sistema para monitorar a propagação

As exibições do sistema a seguir mostram o status da propagação automática do SQL Server.

**sys.dm_hadr_automatic_seeding** 

Na réplica primária, consulte `sys.dm_hadr_automatic_seeding` para verificar o status do processo de propagação automática. A exibição retorna uma linha para cada processo de propagação. Por exemplo:

```sql
SELECT start_time, 
    completion_time
    is_source,
    current_state,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding
```
 
**sys.dm_hadr_physical_seeding_stats** 

Na réplica primária, consulte `sys.dm_hadr_physical_seeding_stats` DMV para ver as estatísticas físicas de cada processo de propagação que está sendo executado no momento. A seguinte consulta retorna linhas quando a propagação está em execução:

```sql
SELECT * FROM sys.dm_hadr_physical_seeding_stats;
```

As duas colunas *total_disk_io_wait_time_ms* e a *total_network_wait_time_ms* podem ser usadas para determinar um gargalo de desempenho no Processo de propagação automática. As duas colunas também estão presentes no evento estendido *hadr_physical_seeding_progress*.

**total_disk_io_wait_time_ms** representa o tempo gasto pelo thread de backup/restauração enquanto aguarda no disco. Esse valor é cumulativo desde o início da operação de propagação. Se os discos não estiverem prontos para ler ou gravar o fluxo de backup, o thread de backup/restauração fará a transição para um estado de suspensão e será ativado a cada um segundo para verificar se o disco está pronto.
        
**total_network_wait_time_ms** é interpretado de maneira diferente para a réplica primária e secundária. Na réplica primária, esse contador representa o tempo de controle do fluxo de rede. Na réplica secundária, isso representa o tempo em que o thread de restauração está aguardando até que uma mensagem esteja disponível para gravação no disco.

### <a name="diagnose-database-initialization-using-automatic-seeding-in-the-error-log"></a>Diagnosticar a inicialização do banco de dados usando a propagação automática no log de erros

Quando você adiciona um banco de dados a um grupo de disponibilidade configurado para a propagação automática, o SQL Server executa um backup da VDI no ponto de extremidade do grupo de disponibilidade. Examine o log de erros do SQL Server para obter informações sobre quando o backup foi concluído e quando o secundário foi sincronizado.

### <a name="diagnose-database-level-health-with-extended-events"></a>Diagnosticar a integridade no nível do banco de dados com os eventos estendidos

A propagação automática tem novos eventos estendidos para acompanhar a alteração de estado, as falhas e as estatísticas de desempenho durante a inicialização. 

Por exemplo, este script cria uma sessão de eventos estendidos que captura eventos relacionados à propagação automática: 

```sql
CREATE EVENT SESSION [AlwaysOn_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(
        SET filename=N'autoseed.xel',
            max_file_size=(5),
            max_rollover_files=(4)
        )
WITH (
    MAX_MEMORY=4096 KB,
    EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
    MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,
    MEMORY_PARTITION_MODE=NONE,
    TRACK_CAUSALITY=OFF,
    STARTUP_STATE=ON
    )
GO 

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO 
```


A seguinte tabela lista os eventos estendidos relacionados à propagação automática: 

| Nome | DESCRIÇÃO|
|------------ |---------------| 
|hadr_db_manager_seeding_request_msg |  Mensagem de solicitação de propagação.
|hadr_physical_seeding_backup_state_change |    Alteração de estado lateral de backup da propagação física.
|hadr_physical_seeding_restore_state_change |Alteração de estado lateral de restauração da propagação física.
|hadr_physical_seeding_forwarder_state_change | Alteração de estado lateral do encaminhador da propagação física.
|hadr_physical_seeding_forwarder_target_state_change |  Alteração de estado lateral do destino do encaminhador da propagação física.
|hadr_physical_seeding_submit_callback  |Evento de retorno de chamada de envio da propagação física.
|hadr_physical_seeding_failure  |Evento de falha da propagação física.
|hadr_physical_seeding_progress |   Evento de progresso da propagação física.
|hadr_physical_seeding_schedule_long_task_failure   |Evento de falha da tarefa longa de agendamento da propagação física.
|hadr_automatic_seeding_start   |Ocorre quando uma operação de propagação automática é enviada.
|hadr_automatic_seeding_state_transition    |Ocorre quando uma operação de propagação automática altera o estado.
|hadr_automatic_seeding_success |Ocorre quando uma operação de propagação automática é bem-sucedida.
|hadr_automatic_seeding_failure |Ocorre quando uma operação de propagação automática falha.
|hadr_automatic_seeding_timeout |Ocorre quando uma operação de propagação automática atinge o tempo limite.

### <a name="other-troubleshooting-considerations"></a>Outras considerações sobre solução de problemas

**Monitorar no momento da propagação automática**

Consulte `sys.dm_hadr_physical_seeding_stats` para obter os processos de propagação automática em execução. A exibição retorna uma linha para cada banco de dados. Por exemplo:

```sql
SELECT local_database_name, 
    role_desc, 
    internal_state_desc, 
    transfer_rate_bytes_per_second, 
    transferred_size_bytes, 
    database_size_bytes, 
    start_time_utc, 
    end_time_utc, estimate_time_complete_utc, 
    total_disk_io_wait_time_ms, 
    total_network_wait_time_ms, 
    is_compression_enabled 
FROM sys.dm_hadr_physical_seeding_stats
```

**Solução de problemas de falha na exibição de um banco de dados em um grupo de disponibilidade configurado para propagação automática**


Quando um banco de dados não aparece como parte de um grupo de disponibilidade com a propagação automática habilitada, provavelmente, a propagação automática falhou. Isso impede a adição do banco de dados ao grupo de disponibilidade nas réplicas primária e secundária. Consulte `sys.dm_hadr_automatic_seeding` nas réplicas primária e secundária. Por exemplo, execute a consulta a seguir para identificar o estado de falha da propagação automática.

```sql
SELECT start_time, 
    completion_time, 
    is_source, 
    current_state, 
    failure_state, 
    failure_state_desc, 
    error_code 
FROM sys.dm_hadr_automatic_seeding
```

## <a name="automatic-seeding-and-performance-considerations"></a>Considerações sobre desempenho e propagação automática

O SQL Server usa um número fixo de threads para a propagação automática. Na instância primária, o SQL Server usa um thread por LUN para ler as alterações. Na instância secundária, o SQL Server usa um thread por LUN para inicializar o banco de dados.

Defina o sinalizador de rastreamento 9567 na réplica primária para habilitar a compactação do fluxo de dados durante a propagação automática. Isso pode reduzir de forma significativa o tempo de transferência da propagação automática. No entanto, também aumenta o uso da CPU. Para obter mais informações, veja [Ajustar a compactação do grupo de disponibilidade](../../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md). 


## <a name="when-not-to-use-automatic-seeding"></a>Quando não usar a propagação automática

Em alguns cenários, a propagação automática pode não ser ideal para inicializar uma réplica secundária. Durante a propagação automática, o SQL Server executa um backup pela rede para a inicialização. Esse processo poderá ser lento se os bancos de dados forem muito grandes ou se a réplica secundária estiver remota. O log de transações desses bancos de dados não poderá ser truncado durante o processo de backup e, portanto, um processo de inicialização longo em um banco de dados ocupado poderá resultar em um aumento significativo do log de transações.
Antes de adicionar um banco de dados a um grupo de disponibilidade com propagação automática, avalie o tamanho do banco de dados, a carga e a distância de sites entre as réplicas.

## <a name="resources"></a>Recursos

[CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)

[Guia de solução de problemas e monitoramento dos grupos de disponibilidade AlwaysOn](/previous-versions/sql/sql-server-guides/dn135328(v=sql.110))