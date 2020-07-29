---
title: Monitorar e solucionar problemas do PolyBase | Microsoft Docs
description: Para solucionar problemas do PolyBase, use essas exibições e DMVs. Ver o plano de consulta do PolyBase, monitorar nós em um grupo do PolyBase e configurar a alta disponibilidade para o nó de nome do Hadoop.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: a6ea70d3e24d659337c85895946c1f310e045234
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247299"
---
# <a name="monitor-and-troubleshoot-polybase"></a>Monitorar e solucionar problemas do PolyBase

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Para solucionar problemas do PolyBase, use as técnicas encontradas neste tópico.

## <a name="catalog-views"></a>Exibições do catálogo

Use as exibições do catálogo listadas aqui para gerenciar as operações de PolyBase.

|Visualizar|Descrição|  
|-|-|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|Identifica tabelas externas.|  
|[sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|Identifica fontes de dados externas.|  
|[sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|Identifica formatos de arquivo externos.|  

## <a name="dynamic-management-views"></a>Exibições de Gerenciamento Dinâmico  

:::row:::
    :::column:::
        [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

As consultas do PolyBase são divididas em uma série de etapas em sys.dm_exec_distributed_request_steps. A tabela a seguir fornece um mapeamento do nome da etapa ao DMV associado.

|Etapa do PolyBase|DMV associado|  
|-|-|
|HadoopJobOperation | sys.dm_exec_external_operations|
|RandomIdOperation | sys.dm_exec_distributed_request_steps|
|HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
|StreamingReturnOperation | sys.dm_exec_dms_workers|
|OnOperation | sys.dm_exec_distributed_sql_requests |

## <a name="to-monitor-polybase-queries-using-dmvs"></a>Para monitorar consultas do PolyBase usando DMVs

Monitorar e solucionar problemas de consultas do PolyBase usando as DMVs a seguir.

1. **Localizar as consultas mais longas em execução**  

   Registre a ID de execução da consulta mais longa em execução.

   ```sql
    -- Find the longest running query  
   SELECT execution_id, st.text, dr.total_elapsed_time  
   FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
   ORDER BY total_elapsed_time DESC;  
   ```

1. **Localize a etapa de execução mais longa da consulta distribuída**  

   Use a ID de execução registrada na etapa anterior. Registre o índice da etapa a etapa mais longa em execução.

   Verifique o location_type da etapa mais longa em execução:  

   - Cabeçalho ou cálculo: implica uma operação de SQL. Vá para a etapa 3a.

      - DMS: implica uma operação de serviço de movimentação de dados do PolyBase. Vá para a etapa 3b.

      ```sql  
      -- Find the longest running step of the distributed query plan  
      SELECT execution_id, step_index, operation_type, distribution_type,   
      location_type, status, total_elapsed_time, command   
      FROM sys.dm_exec_distributed_request_steps   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;  
      ```  

1. **Registre o andamento da execução da etapa de execução mais longa**  

   1. **Localizar o andamento da execução de uma etapa SQL**  

      Use a ID de execução e o índice de etapa registrados nas etapas anteriores. Use a ID de execução e o índice de etapa registrados nas etapas anteriores.

      ```sql  
      -- Find the execution progress of SQL step    
      SELECT execution_id, step_index, distribution_id, status,   
      total_elapsed_time, row_count, command   
      FROM sys.dm_exec_distributed_sql_requests   
      WHERE execution_id = 'QID4547' and step_index = 1;  
      ```  

   1. **Localizar o andamento da execução de uma etapa DMS**

      Use a ID de execução e o índice de etapa registrados nas etapas anteriores.

      ```sql  
      -- Find the execution progress of DMS step    
      SELECT execution_id, step_index, dms_step_index, status,   
      type, bytes_processed, total_elapsed_time  
      FROM sys.dm_exec_dms_workers   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;
      ```  

1. **Localizar as informações sobre operações de DMS externas**  

   Use a ID de execução e o índice de etapa registrados nas etapas anteriores.

   ```sql  
   SELECT execution_id, step_index, dms_step_index, compute_node_id,   
   type, input_name, length, total_elapsed_time, status   
   FROM sys.dm_exec_external_work   
   WHERE execution_id = 'QID4547' and step_index = 7   
   ORDER BY total_elapsed_time DESC;  
   ```  

## <a name="to-view-the--polybase-query-plan-to-be-changed"></a>Para exibir o plano de consulta do PolyBase (a ser alterado) 

1. No SSMS, habilite **Incluir Plano de Execução Real** (Ctrl + M) e execute a consulta.

2. Clique na guia **Plano de execução** .

   ![Plano de consulta do PolyBase](../../relational-databases/polybase/media/polybase-query-plan.png "Plano de consulta do PolyBase")  

3. Clique com o botão direito do mouse no **Operador de Consulta Remota** e selecione **Propriedades**.

4. Copie e cole o valor da consulta remota em um editor de texto para exibir o plano de consulta remota de XML. Um exemplo é mostrado abaixo.

   ```xml  

   <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
             [T1_1].[CustomerKey] AS [CustomerKey],  
             [T1_1].[GeographyKey] AS [GeographyKey],  
             [T1_1].[Speed] AS [Speed],  
             [T1_1].[YearMeasured] AS [YearMeasured]  
      FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                     [T2_1].[CustomerKey] AS [CustomerKey],  
                     [T2_1].[GeographyKey] AS [GeographyKey],  
                     [T2_1].[Speed] AS [Speed],  
                     [T2_1].[YearMeasured] AS [YearMeasured]  
              FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
              WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
   </dsql_query>  
   ```  

## <a name="to-monitor-nodes-in-a-polybase-group"></a>Para monitorar nós em um grupo de PolyBase  

Depois de configurar um conjunto de computadores como parte de um grupo de escala horizontal do PolyBase, você pode monitorar o status dos computadores. Para obter detalhes sobre como criar um grupo de escala horizontal, veja [Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).

1. Conecte-se ao SQL Server no nó principal de um grupo.

2. Execute a DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) para exibir todos os nós do Grupo do PolyBase.

3. Execute a DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) para exibir o status de todos os nós do Grupo do PolyBase.

## <a name="hadoop-name-node-high-availability"></a>Alta disponibilidade do nó de nome do Hadoop

O PolyBase não estabelece uma interface com os serviços de HA do nó de nome como o Zookeeper ou o Knox atualmente. No entanto, há uma solução comprovada que pode ser usada para fornecer a funcionalidade.

Solução alternativa: use o nome DNS para redirecionar conexões para o Nó de Nome ativo. Para fazer isso, você precisará garantir que a fonte de dados externa esteja usando um nome DNS para se comunicar com o nó de nome. Quando ocorrer o failover do nó de nome, você precisará alterar o endereço IP associado ao nome DNS usado na definição de fonte de dados externa. Isso redirecionará todas as novas conexões para o nó de nome correto. As conexões existentes falharão quando ocorrer failover. Para automatizar esse processo, uma "pulsação" pode executar o ping no nó de nome ativo. Se a pulsação falha, é possível assumir que um failover ocorreu e alternar automaticamente para o endereço IP secundário.

## <a name="error-messages-and-possible-solutions"></a>Mensagens de erro e possíveis soluções

Para solucionar problemas de erros de tabela externa, confira o blog de Murshed Zaman [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "Erros de instalação do PolyBase e possíveis soluções").

## <a name="see-also"></a>Confira também

[Solucionar problemas de conectividade do PolyBase Kerberos](polybase-troubleshoot-connectivity.md)
