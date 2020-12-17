---
title: Criar um pool de recursos
description: Saiba como você pode criar e usar um pool de recursos para gerenciar cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: da6f6817856efd9dd0310211998230d49e6f3d1b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471387"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>Criar um pool de recursos para os Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Saiba como você pode criar e usar um pool de recursos para gerenciar cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server. 

O processo inclui várias etapas:

1. Verificar o status dos pools de recursos existentes. É importante entender quais serviços estão usando recursos existentes.
2. Modificar pools de recursos do servidor.
3. Criar um novo pool de recursos para processos externos.
4. Criar uma função de classificação para identificar solicitações de script externas.
5. Verificar se o novo pool de recursos externos está capturando trabalhos de R ou Python dos clientes ou contas especificados.

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>Verificar o status dos pools de recursos existentes
  
1.  Use uma instrução como a exibida a seguir para verificar os recursos atribuídos ao pool padrão do servidor.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Resultados de exemplo**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|padrão|0|100|0|100|100|0|0|

2.  Verifique os recursos atribuídos ao pool de recursos **externo** padrão.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Resultados de exemplo**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|padrão|100|20|0|2|
 
3.  Sob essas configurações padrão do servidor, o runtime externo provavelmente terá recursos insuficientes para concluir a maioria das tarefas. Para melhorar os recursos, modifique o uso de recursos de servidor da seguinte maneira:
  
    -   Reduzir a memória máxima do computador que pode ser usada pelo mecanismo de banco de dados.
  
    -   Aumentar a memória máxima do computador que pode ser usada pelo processo externo.

## <a name="modify-server-resource-usage"></a>Modificar o uso de recursos do servidor

1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução para limitar o uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **60%** do valor na configuração de 'memória máxima do servidor'.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2. Execute a instrução a seguir para limitar o uso de memória por processos externos para **40%** dos recursos totais do computador.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  Para aplicar essas alterações, você deve reconfigurar e reiniciar o Resource Governor da seguinte maneira:
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  Essas são apenas configurações sugeridas para começar. Você deve avaliar suas tarefas de aprendizado de máquina em relação a outros processos do servidor para determinar o equilíbrio correto para seu ambiente e sua carga de trabalho.

## <a name="create-a-user-defined-external-resource-pool"></a>Criar um pool de recursos externo definido pelo usuário
  
1.  Todas as alterações na configuração de Resource Governor são impostas pelo servidor como um todo. As alterações afetam as cargas de trabalho que usam os pools padrão para o servidor, bem como as cargas de trabalho que usam os pools externos.
  
     Para fornecer um controle mais refinado sobre quais cargas de trabalho devem ter precedência, você pode criar um pool de recursos externos definido pelo usuário. Defina uma função de classificação e a atribua ao pool de recursos externos. A palavra-chave **EXTERNAL** é nova.
  
     Crie um *pool de recursos externo definido pelo usuário*. No exemplo a seguir, o pool é denominado **ds_ep**.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  Crie um grupo de carga de trabalho chamado `ds_wg` para usar em solicitações de sessão de gerenciamento. Para consultas SQL, você usará o pool padrão. Para todos as consultas de processos externos você usará o pool `ds_ep`.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     As solicitações são atribuídas ao grupo padrão sempre que a solicitação não pode ser classificada ou caso haja qualquer outra falha de classificação.

 
Para obter mais informações, consulte [Grupo de carga de trabalho do Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md) e [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).
  
## <a name="create-a-classification-function-for-machine-learning"></a>Criar uma função de classificação para aprendizado de máquina
  
Uma função de classificação examina as tarefas recebidas. Ela determina se a tarefa é do tipo que pode ser executada usando o pool de recursos atual. As tarefas que não atendem aos critérios da função de classificação são atribuídas de volta ao pool de recursos padrão do servidor.
  
1. Comece especificando que uma função de classificação deve ser usada pelo Resource Governor para determinar os pools de recursos. Você pode atribuir **null** como um espaço reservado para a função de classificação.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  Na função de classificação para cada pool de recursos, defina o tipo de instruções ou solicitações de entrada que devem ser atribuídas ao pool de recursos.
  
     Por exemplo, a função a seguir retornará o nome do esquema atribuído ao pool de recursos externo definido pelo usuário se o aplicativo que enviou a solicitação for 'Microsoft R Host', 'RStudio' ou 'Mashup'. Caso contrário, ela retornará o pool de recursos padrão.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio', 'Mashup') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Quando a função tiver sido criada, reconfigure o grupo de recursos para atribuir a nova função de classificação para o grupo de recursos externos que você definiu anteriormente.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Verificar os novos pools de recursos e a afinidade

Verifique a configuração de memória do servidor e a CPU de cada um dos grupos de carga de trabalho. Para verificar se as alterações de recurso de instância foram feitas, examine:

+ o pool padrão para o servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ o pool de recursos padrão para processos externos
+ o pool definido pelo usuário para processos externos

1. Execute a seguinte instrução para exibir todos os grupos de carga de trabalho:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Resultados de exemplo**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|interno|Médio|25|0|0|0|0|1|2|
    |2|default|Médio|25|0|0|0|0|2|2|
    |256|ds_wg|Médio|25|0|0|0|0|2|256|
  
2.  Use a nova exibição de catálogo, [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para exibir todos os pools de recursos externos.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Resultados de exemplo**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Para obter mais informações, consulte [Exibições de catálogo do Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).
  
3.  Execute a instrução a seguir para retornar informações sobre os recursos do computador que são relacionados ao pool de recursos externos, se aplicável:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     Nenhuma informação será exibida porque os grupos foram criados com uma afinidade AUTO. Para obter mais informações, consulte [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o gerenciamento de recursos do servidor, confira:

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 
+ [Exibições de gerenciamento dinâmico relacionadas ao Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Para ter uma visão geral da governança de recursos para aprendizado de máquina, confira:

+ [Gerenciar cargas de trabalho do Python e do R com o Resource Governor nos Serviços de Machine Learning do SQL Server](resource-governor.md)
