---
title: Monitorando o desempenho usando o Repositório de Consultas | Microsoft Docs
description: O Repositório de Consultas do SQL Server fornece insights sobre a escolha e o desempenho do plano de consulta. O Repositório de Consultas captura o histórico de consultas, planos e estatísticas do runtime.
ms.custom: ''
ms.date: 04/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest
ms.openlocfilehash: e61f723ddbc3010cc705c076675b731482fdee6b
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98171838"
---
# <a name="monitoring-performance-by-using-the-query-store"></a>Monitorar o desempenho usando o Repositório de Consultas

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

O recurso Repositório de Consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece informações sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, ajudando você a identificar rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O Repositório de Consultas captura automaticamente um histórico das consultas, dos planos e das estatísticas de runtime e os mantém para sua análise. Ele separa os dados por janelas por hora, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas pode ser configurado usando a opção [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) .

Para obter informações sobre como operar o Repositório de Consultas no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] do Azure, consulte [Operando o Repositório de Consultas no Banco de dados SQL do Azure](best-practice-with-the-query-store.md#Insight).

> [!IMPORTANT]
> Se você estiver usando o Repositório de Consultas para obter informações de carga de trabalho em tempo real no [!INCLUDE[ssSQL15](../../includes/sssql16-md.md)], planeje instalar as correções de escalabilidade de desempenho na [KB 4340759](https://support.microsoft.com/help/4340759) assim que possível.

## <a name="enabling-the-query-store"></a><a name="Enabling"></a> Habilitando o Repositório de Consultas

 O Repositório de Consultas não está habilitado por padrão em novos bancos de dados do SQL Server e do Azure Synapse Analytics e está habilitado por padrão em novos bancos de dados do Banco de Dados SQL do Azure.

### <a name="use-the-query-store-page-in-ssmanstudiofull"></a>Use a Página do Repositório de Consultas em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

1. No Pesquisador de Objetos, clique com o botão direito do mouse em um banco de dados e clique em **Propriedades**.

   > [!NOTE]
   > Exige, no mínimo, a versão 16 do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

2. Na caixa de diálogo **Propriedades do Banco de Dados** , selecione a página **Repositório de Consultas** .

3. Na caixa **Modo de Operação (Solicitado)** , selecione **Leitura Gravação**.

### <a name="use-transact-sql-statements"></a>Usar Instruções Transact-SQL

Use a instrução **ALTER DATABASE** para habilitar o repositório de consultas para um determinado banco de dados. Por exemplo:

```sql
SET QUERY_STORE = ON (OPERATION_MODE = READ_WRITE);
```

Para obter mais opções de sintaxe relacionadas ao Repositório de Consultas, confira [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).

> [!NOTE]
> O Repositório de Consultas não pode ser habilitado nos bancos de dados **mestre** ou **tempdb**.

> [!IMPORTANT]
> Para obter informações sobre como habilitar o Repositório de Consultas e mantê-lo ajustado a sua carga de trabalho, consulte [Melhor Prática do Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure).

## <a name="information-in-the-query-store"></a><a name="About"></a> Informações no Repositório de Consultas

Planos de execução para qualquer consulta específica no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente envolvem horas extras por vários motivos diferentes, como alterações de estatísticas, alterações de esquema, criação/exclusão de índices, etc. O cache de procedimento (no qual os planos de consulta em cache são armazenados) armazena apenas o plano de execução mais recente. Os planos também são removidos do cache do plano devido à pressão da memória. Como resultado, as regressões do desempenho de consulta causadas por alterações no plano de execução podem não ser triviais e podem ter resolução lenta.

Como o Repositório de Consultas mantém vários planos de execução por consulta, ele pode impor políticas para instruir o Processador de Consultas a usar um plano de execução específico para uma consulta. Isso é conhecido como imposição de plano. A imposição de plano no repositório de consultas é fornecida usando um mecanismo semelhante à dica de consulta [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) , mas não requer nenhuma alteração nos aplicativos do usuário. A imposição de plano pode resolver uma regressão de desempenho de consulta causada por uma alteração do plano em um período muito curto.

> [!NOTE]
> O Repositório de Consultas coleta planos para Instruções DML, como SELECT, INSERT, UPDATE, DELETE, MERGE e BULK INSERT.
>
> O Repositório de Consultas não coleta dados para procedimentos armazenados compilados nativamente por padrão. Use [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) para habilitar a coleta de dados para procedimentos armazenados compilados nativamente.

As **estatísticas de espera** são outra fonte de informações que ajudam a solucionar problemas de desempenho no [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Por muito tempo, as estatísticas de espera estavam disponíveis somente no nível da instância, o que dificultava o retorno das esperas de uma consulta específica. No [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] em diante, o Repositório de Consultas inclui uma dimensão que acompanha as estatísticas de espera. O exemplo a seguir habilita o Repositório de Consultas para coletar estatísticas de espera.

```sql
SET QUERY_STORE = ON ( WAIT_STATS_CAPTURE_MODE = ON );
```

Cenários comuns para o uso do recurso Repositório de Consultas são:

- Localizar e corrigir rapidamente uma regressão de desempenho do plano, forçando o plano de consulta anterior. Corrigir consultas com regressão recente no desempenho devido a alterações no plano de execução.
- Determinar o número de vezes que uma consulta foi executada em determinada janela de tempo, auxiliando um DBA na solução de problemas de recurso de desempenho.
- Identificar as principais consultas *n* (por tempo de execução, consumo de memória, etc.) nas últimas *x* horas.
- Fazer auditoria de histórico dos planos de consulta para determinada consulta.
- Analisar os padrões de uso dos recursos (CPU, E/S e memória) para determinado banco de dados.
- Identifique as principais n consultas que estão esperando em recursos.
- Entenda a natureza de espera de um plano ou de uma consulta específica.

O Repositório de Consultas contém três repositórios:

- um **repositório de plano** para persistir as informações do plano de execução.
- um **repositório de estatísticas de runtime** para manter as informações de estatísticas de execução.
- um **repositório de estatísticas de espera** para manter as informações de estatísticas de espera.

O número de planos exclusivos que pode ser armazenado para uma consulta no repositório de planos é limitado pela opção de configuração **max_plans_per_query** . Para melhorar o desempenho, as informações são gravadas nos repositórios de forma assíncrona. Para otimizar o uso do espaço, as estatísticas de runtime no repositório de estatísticas de runtime são agregadas em uma janela de tempo fixa. As informações nesses repositórios são visíveis pela consulta das exibições de catálogo do Repositório de Consultas.

A consulta a seguir retorna informações sobre consultas e planos no Repositório de Consultas.

```sql
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
FROM sys.query_store_plan AS Pl
INNER JOIN sys.query_store_query AS Qry
    ON Pl.query_id = Qry.query_id
INNER JOIN sys.query_store_query_text AS Txt
    ON Qry.query_text_id = Txt.query_text_id ;
```

## <a name="use-the-regressed-queries-feature"></a><a name="Regressed"></a> Usar o recurso Consultas Regredidas

Depois de habilitar o Repositório de Consultas, atualize a parte do banco de dados do painel Pesquisador de Objetos para adicionar a seção **Repositório de Consultas**.

![Árvore de Repositório de Consultas do SQL Server 2016 no Pesquisador de Objetos do SSMS](../../relational-databases/performance/media/objectexplorerquerystore.PNG "Árvore de Repositório de Consultas do SQL Server 2016 no Pesquisador de Objetos do SSMS") ![Árvore de Repositório de Consultas do SQL Server 2017 no Pesquisador de Objetos do SSMS](../../relational-databases/performance/media/objectexplorerquerystore_sql17.PNG "Árvore de Repositório de Consultas do SQL Server 2017 no Pesquisador de Objetos do SSMS")

Selecione **Consultas Regredidas** para abrir o painel **Consultas Regredidas** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O painel Consultas Regredidas mostra consultas e planos no repositório de consultas. Use as caixas de listas suspensas na parte superior para filtrar consultas com base em vários critérios: **Duração (ms)** (Padrão), Tempo de CPU (ms), Leituras Lógicas, Gravações Lógicas (KB), Leituras Físicas (KB), Tempo CLR (ms), DOP, Consumo de Memória (KB), Contagem de Linhas, Memória de Log Usada (KB), Memória de BD Temporária Usada (KB) e Tempo de Espera (ms).

Selecione um plano para ver o plano de consulta gráfico. Há botões disponíveis para exibir a consulta de origem, para forçar e não forçar um plano de consulta, para alternar entre os formatos de grade e gráfico, para comparar os planos selecionados (se houver mais de um selecionado) e para atualizar a exibição.

![Consultas Retornadas do SQL Server 2016 no Pesquisador de Objetos do SSMS](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "Consultas Retornadas do SQL Server 2016 no Pesquisador de Objetos do SSMS")

Para impor um plano, selecione uma consulta e um plano e, em seguida, clique em **Impor Plano.** Você pode impor apenas planos que foram salvos pelo recurso de plano de consulta e ainda são mantidos no cache do plano de consulta.

## <a name="finding-waiting-queries"></a><a name="Waiting"></a> Como localizar consultas em espera

No [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] em diante, as estatísticas de espera por consulta ao longo do tempo estão disponíveis no Repositório de Consultas.

No Repositório de Consultas, os tipos de espera são combinados em **categorias de espera**. O mapeamento das categorias de espera para tipos de espera está disponível em [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md#wait-categories-mapping-table).

Selecione **Estatísticas de Espera da Consulta** para abrir o painel **Estatísticas de Espera da Consulta** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18 ou superior. O painel Estatísticas de Espera da Consulta mostra a você um gráfico de barras que contém os principais categorias de espera no Repositório de Consultas. Use lista suspensa na parte superior para selecionar um critério de agregação para o tempo de espera: avg, max, min, std dev e **total** (padrão).

![Estatísticas de espera de consulta do SQL Server 2017 no Pesquisador de Objetos do SSMS](../../relational-databases/performance/media/query-store-waits.PNG "Estatísticas de espera de consulta do SQL Server 2017 no Pesquisador de Objetos do SSMS")

Selecione uma categoria de espera clicando na barra e uma exibição de detalhes é mostrada na categoria de espera selecionada. Esse novo gráfico de barras contém as consultas que contribuíram para essa categoria de espera.

![Exibição de detalhes das Estatísticas de espera de consulta do SQL Server 2017 no Pesquisador de Objetos do SSMS](../../relational-databases/performance/media/query-store-waits-detail.PNG "Exibição de detalhes das Estatísticas de espera de consulta do SQL Server 2017 no Pesquisador de Objetos do SSMS")

Use a lista suspensa na parte superior para filtrar consultas com base em vários critérios de tempo de espera para a categoria de espera selecionada: avg, max, min, std dev e **total** (padrão). Selecione um plano para ver o plano de consulta gráfico. Botões estão disponíveis para exibir a consulta de origem, impor e cancelar a imposição de um plano de consulta e atualizar a exibição.

As **categorias de espera** combinam tipos diferentes de espera em buckets semelhantes por natureza. Categorias de espera diferentes exigem um acompanhamento de análise diferente para resolver o problema, mas os tipos de espera da mesma categoria levam a experiências de solução de problemas muito semelhantes e fornecer a consulta afetada com base nas esperas seria a peça que faltava para concluir a maioria dessas investigações de com êxito.

Aqui estão alguns exemplos de como você pode obter mais informações sobre sua carga de trabalho antes e depois de introduzir as categorias de espera no Repositório de Consultas:

|Experiência anterior|Nova experiência|Ação|
|-|-|-|
|RESOURCE_SEMAPHORE alto de esperas por banco de dados|Esperas de memória alta no Repositório de Consultas para consultas específicas|Localize as consultas que consomem mais memória no Repositório de Consultas. Essas consultas estão provavelmente atrasando o andamento das consultas afetadas. Considere usar a dica de consulta MAX_GRANT_PERCENT para essas consultas ou para as consultas afetadas.|
|Espera de LCK_M_X alta por banco de dados|Esperas de bloqueio altas no Repositório de Consultas para consultas específicas|Verifique os textos de consulta para as consultas afetadas e identifique as entidades de destino. Pesquise outras consultas no Repositório de Consultas que modificam a mesma entidade, que são executadas com frequência e/ou têm alta duração. Depois de identificar essas consultas, considere alterar a lógica do aplicativo para melhorar a simultaneidade ou use um nível de isolamento menos restritivo.|
|Esperas de PAGEIOLATCH_SH altas por banco de dados|Esperas de buffer de E/S altas no Repositório de Consultas para consultas específicas|Localize as consultas com um grande número de leituras físicas no Repositório de Consultas. Se elas corresponderem às consultas com esperas de E/S, considere introduzir um índice na entidade subjacente, para fazer buscas em vez de verificações e, portanto, minimizar a sobrecarga de E/S das consultas.|
|Esperas de SOS_SCHEDULER_YIELD altas por banco de dados|Esperas de CPU altas no Repositório de Consultas para consultas específicas|Localize as consultas com maior consumo de CPU no Repositório de Consultas. Entre elas, identifique as consultas para as quais a tendência de CPU alta se correlaciona às esperas de CPU altas para as consultas afetadas. Concentre-se em otimizar essas consultas – poderia haver uma regressão de plano ou talvez um índice ausente.|

## <a name="configuration-options"></a><a name="Options"></a> Opções de configuração

Para obter as opções disponíveis a fim de configurar os parâmetros do Repositório de Consultas, confira [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md#query-store).

Consulte a exibição **sys.database_query_store_options** para determinar as opções atuais do Repositório de Consultas. Para obter mais informações sobre os valores, consulte [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).

Para obter exemplos de como definir as opções de configuração usando as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], confira o [Gerenciamento de opções](#OptionMgmt).

## <a name="related-views-functions-and-procedures"></a><a name="Related"></a> Exibições, Funções e Procedimentos Relacionados

Exiba e gerencie o Repositório de Consultas por meio do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou usando as exibições e os procedimentos a seguir.

### <a name="query-store-functions"></a>Funções do Repositório de Consultas

As funções ajudam as operações com o Repositório de Consultas.

:::row:::
    :::column:::
        [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="query-store-catalog-views"></a>Exibições do catálogo de repositório de consulta

As exibições do catálogo apresentam informações sobre o Repositório de Consultas.

:::row:::
    :::column:::
        [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
    :::column-end:::
:::row-end:::


### <a name="query-store-stored-procedures"></a>Procedimentos armazenados do repositório de consulta

Os procedimentos armazenados configuram o Repositório de Consultas.

:::row:::
    :::column:::
        [sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_query_store_remove_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)
    :::column-end:::
    :::column:::
        [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        sp_query_store_consistency_check &#40;Transact-SQL&#41;<sup>1</sup>
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

<sup>1</sup> Em cenários extremos, o Repositório de Consultas pode inserir um estado de ERRO devido a erros internos. Do SQL Server 2017 (14.x) em diante, se isso acontecer, o Repositório de Consultas poderá ser recuperado por meio da execução do procedimento armazenado sp_query_store_consistency_check no banco de dados afetado. Confira [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para obter mais detalhes especificados na descrição da coluna actual_state_desc.

## <a name="key-usage-scenarios"></a><a name="Scenarios"></a> Principais cenários de uso

### <a name="option-management"></a><a name="OptionMgmt"></a> Gerenciamento de opção

Esta seção fornece algumas diretrizes sobre como gerenciar recursos do próprio repositório de consultas.

**O Repositório de Consultas está ativo no momento?**

O Repositório de Consultas armazena seus dados dentro do banco de dados do usuário e é por isso que ele tem limite de tamanho (configurado com `MAX_STORAGE_SIZE_MB`). Se os dados no repositório de consultas atingirem esse limite, o repositório de consultas alterará automaticamente o status de somente gravação para somente leitura e interromperá a coleta de novos dados.

Consulte [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para determinar se o Repositório de Consultas está ativo no momento e se está coletando estatísticas de runtime ou não.

```sql
SELECT actual_state, actual_state_desc, readonly_reason,
    current_storage_size_mb, max_storage_size_mb
FROM sys.database_query_store_options;
```

O status do Repositório de Consultas é determinado pela coluna actual_state. Caso não seja o status desejado, a coluna `readonly_reason` pode fornecer mais informações.
Quando o tamanho do Repositório de Consultas exceder a cota, o recurso passará para o modo de read_only.

**Opções Obter Repositório de Consultas**

Para obter informações detalhadas sobre o status do repositório de consultas, execute o seguinte em um banco de dados do usuário.

```sql
SELECT * FROM sys.database_query_store_options;
```

**Configurar o intervalo do Repositório de Consultas**

Você pode substituir o intervalo para agregar estatísticas de runtime de consulta (o padrão é 60 minutos).

```sql
ALTER DATABASE <database_name>
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);
```

> [!NOTE]
> Não são permitidos valores arbitrários para `INTERVAL_LENGTH_MINUTES`. Use um dos seguintes: 1, 5, 10, 15, 30, 60 ou 1.440 minutos.

O novo valor do intervalo é exposto por meio da exibição **sys.database_query_store_options** .

**Uso de espaço do Repositório de Consultas**

Para verificar o tamanho atual e o limite do Repositório de Consultas, execute a instrução a seguir no banco de dados do usuário.

```sql
SELECT current_storage_size_mb, max_storage_size_mb
FROM sys.database_query_store_options;
```

Se o armazenamento do repositório de consultas estiver completo, use a seguinte instrução para ampliar o armazenamento.

```sql
ALTER DATABASE <database_name>
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);
```

**Definir as opções do Repositório de Consultas**

Você pode definir várias opções de repositório de consultas de uma só vez com uma única instrução ALTER DATABASE.

```sql
ALTER DATABASE <database name>
SET QUERY_STORE (
    OPERATION_MODE = READ_WRITE,
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),
    DATA_FLUSH_INTERVAL_SECONDS = 3000,
    MAX_STORAGE_SIZE_MB = 500,
    INTERVAL_LENGTH_MINUTES = 15,
    SIZE_BASED_CLEANUP_MODE = AUTO,
    QUERY_CAPTURE_MODE = AUTO,
    MAX_PLANS_PER_QUERY = 1000,
    WAIT_STATS_CAPTURE_MODE = ON
);
```

Para obter a lista completa de opções de configuração, confira [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).

**Limpar o espaço**

Tabelas internas do repositório de consultas são criadas no grupo de arquivos PRIMARY durante a criação do banco de dados e essa configuração não pode ser alterada posteriormente. Se você estiver executando sem espaço, limpe os dados antigos do repositório de consultas usando a instrução a seguir.

```sql
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;
```

Você pode também limpar apenas dados de consulta ad hoc, pois são menos relevantes para otimizações de consulta e análise do plano, mas eles ocupam a mesma quantidade de espaço.

**Excluir consultas ad hoc**

Isso limpa as consultas ad hoc e internas do repositório de consultas a cada 3 minutos para que o repositório de consultas não fique sem espaço e remova as consultas que realmente precisamos acompanhar

```sql
SET NOCOUNT ON
-- This purges adhoc and internal queries from the query store every 3 minutes so that the
-- query store does not run out of space and remove queries we really need to track
DECLARE @command varchar(1000)

SELECT @command = 'IF ''?'' NOT IN(''master'', ''model'', ''msdb'', ''tempdb'') BEGIN USE ?
EXEC(''
DECLARE @id int
DECLARE adhoc_queries_cursor CURSOR
FOR
SELECT q.query_id
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
ON q.query_text_id = qt.query_text_id
JOIN sys.query_store_plan AS p
ON p.query_id = q.query_id
JOIN sys.query_store_runtime_stats AS rs
ON rs.plan_id = p.plan_id
WHERE q.is_internal_query = 1 ' -- is it an internal query then we dont care to keep track of it

' OR q.object_id = 0' -- if it does not have a valid object_id then it is an adhoc query and we dont care about keeping track of it
' GROUP BY q.query_id
HAVING MAX(rs.last_execution_time) < DATEADD (minute, -5, GETUTCDATE()) ' -- if it has been more than 5 minutes since the adhoc query ran
' ORDER BY q.query_id ;
OPEN adhoc_queries_cursor ;
FETCH NEXT FROM adhoc_queries_cursor INTO @id;
WHILE @@fetch_status = 0
BEGIN
EXEC sp_query_store_remove_query @id
FETCH NEXT FROM adhoc_queries_cursor INTO @id
END
CLOSE adhoc_queries_cursor ;
DEALLOCATE adhoc_queries_cursor;
'') END' ;
EXEC sp_MSforeachdb @command
```

Você pode definir seu próprio procedimento com uma lógica diferente para limpar os dados que não são mais necessários.

O exemplo acima usa o procedimento armazenado estendido **sp_query_store_remove_query** para remover dados desnecessários. Também é possível usar:

- **sp_query_store_reset_exec_stats** para limpar as estatísticas de runtime para um plano específico.
- **sp_query_store_remove_plan** para remover um único plano.

### <a name="performance-auditing-and-troubleshooting"></a><a name="Peformance"></a> Auditoria e solução de problemas de desempenho

O Repositório de Consultas mantém um histórico das métricas de compilação e de runtime durante as execuções de consulta, permitindo que você faça perguntas sobre sua carga de trabalho.

**Últimas *n* consultas executadas no banco de dados?**

```sql
SELECT TOP 10 qt.query_sql_text, q.query_id,
    qt.query_text_id, p.plan_id, rs.last_execution_time
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p
    ON q.query_id = p.query_id
JOIN sys.query_store_runtime_stats AS rs
    ON p.plan_id = rs.plan_id
ORDER BY rs.last_execution_time DESC;
```

**Número de execuções de cada consulta?**

```sql
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,
    SUM(rs.count_executions) AS total_execution_count
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p
    ON q.query_id = p.query_id
JOIN sys.query_store_runtime_stats AS rs
    ON p.plan_id = rs.plan_id
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text
ORDER BY total_execution_count DESC;
```

**O número de consultas com o tempo médio de execução mais longo na última hora?**

```sql
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,
    rs.last_execution_time
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p
    ON q.query_id = p.query_id
JOIN sys.query_store_runtime_stats AS rs
    ON p.plan_id = rs.plan_id
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())
ORDER BY rs.avg_duration DESC;
```

**O número de consultas que tiveram a maior média de leituras físicas de E/S nas últimas 24 horas, com a média de contagem de linhas e execuções correspondente?**

```sql
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p
    ON q.query_id = p.query_id
JOIN sys.query_store_runtime_stats AS rs
    ON p.plan_id = rs.plan_id
JOIN sys.query_store_runtime_stats_interval AS rsi
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())
ORDER BY rs.avg_physical_io_reads DESC;
```

**Consultas com vários planos?** Essas consultas são especialmente interessantes porque são candidatas a regressões em razão de alteração na escolha do plano. A consulta a seguir identifica essas consultas junto com todos os planos:

```sql
WITH Query_MultPlans
AS
(
SELECT COUNT(*) AS cnt, q.query_id
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p
    ON p.query_id = q.query_id
GROUP BY q.query_id
HAVING COUNT(distinct plan_id) > 1
)

SELECT q.query_id, object_name(object_id) AS ContainingObject,
    query_sql_text, plan_id, p.query_plan AS plan_xml,
    p.last_compile_start_time, p.last_execution_time
FROM Query_MultPlans AS qm
JOIN sys.query_store_query AS q
    ON qm.query_id = q.query_id
JOIN sys.query_store_plan AS p
    ON q.query_id = p.query_id
JOIN sys.query_store_query_text qt
    ON qt.query_text_id = q.query_text_id
ORDER BY query_id, plan_id;
```

 **Consultas com regressão recente de desempenho (comparando diferentes pontos no tempo)?** O exemplo de consulta a seguir retorna todas as consultas para as quais o tempo de execução dobrou nas últimas 48 horas em razão de alteração na escolha do plano. A consulta compara todos os intervalos de estatísticas de runtime lado a lado.

```sql
SELECT
    qt.query_sql_text,
    q.query_id,
    qt.query_text_id,
    rs1.runtime_stats_id AS runtime_stats_id_1,
    rsi1.start_time AS interval_1,
    p1.plan_id AS plan_1,
    rs1.avg_duration AS avg_duration_1,
    rs2.avg_duration AS avg_duration_2,
    p2.plan_id AS plan_2,
    rsi2.start_time AS interval_2,
    rs2.runtime_stats_id AS runtime_stats_id_2
FROM sys.query_store_query_text AS qt
JOIN sys.query_store_query AS q
    ON qt.query_text_id = q.query_text_id
JOIN sys.query_store_plan AS p1
    ON q.query_id = p1.query_id
JOIN sys.query_store_runtime_stats AS rs1
    ON p1.plan_id = rs1.plan_id
JOIN sys.query_store_runtime_stats_interval AS rsi1
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id
JOIN sys.query_store_plan AS p2
    ON q.query_id = p2.query_id
JOIN sys.query_store_runtime_stats AS rs2
    ON p2.plan_id = rs2.plan_id
JOIN sys.query_store_runtime_stats_interval AS rsi2
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())
    AND rsi2.start_time > rsi1.start_time
    AND p1.plan_id <> p2.plan_id
    AND rs2.avg_duration > 2*rs1.avg_duration
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;
```

Para ver todas as regressões de desempenho (não apenas as relacionadas a alteração na escolha do plano), basta remover a condição `AND p1.plan_id <> p2.plan_id` da consulta anterior.

**Consultas que estão aguardando mais?**
Essa consulta retornará as dez principais consultas que mais esperam.

```sql
SELECT TOP 10
    qt.query_text_id,
    q.query_id,
    p.plan_id,
    sum(total_query_wait_time_ms) AS sum_total_wait_ms
FROM sys.query_store_wait_stats ws
JOIN sys.query_store_plan p ON ws.plan_id = p.plan_id
JOIN sys.query_store_query q ON p.query_id = q.query_id
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
GROUP BY qt.query_text_id, q.query_id, p.plan_id
ORDER BY sum_total_wait_ms DESC
```

**Consultas com regressão recente de desempenho (comparando execuções recentes e históricas)?** A próxima consulta compara os períodos de execução baseados na execução da consulta. Nesse exemplo específico, a consulta compara a execução no período recente (uma hora) com o período do histórico (último dia) e identifica as que introduziram o `additional_duration_workload`. Essa métrica é calculada como uma diferença entre a média de execução recente e a média de execução do histórico, multiplicado pelo número de execuções recentes. Representa, na verdade, quanto de duração adicional as execuções recentes introduziram em comparação com histórico:

```sql
--- "Recent" workload - last 1 hour
DECLARE @recent_start_time datetimeoffset;
DECLARE @recent_end_time datetimeoffset;
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());
SET @recent_end_time = SYSUTCDATETIME();

--- "History" workload
DECLARE @history_start_time datetimeoffset;
DECLARE @history_end_time datetimeoffset;
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());
SET @history_end_time = SYSUTCDATETIME();

WITH
hist AS
(
    SELECT
        p.query_id query_id,
        ROUND(ROUND(CONVERT(FLOAT, SUM(rs.avg_duration * rs.count_executions)) * 0.001, 2), 2) AS total_duration,
        SUM(rs.count_executions) AS count_executions,
        COUNT(distinct p.plan_id) AS num_plans
     FROM sys.query_store_runtime_stats AS rs
        JOIN sys.query_store_plan AS p ON p.plan_id = rs.plan_id
    WHERE (rs.first_execution_time >= @history_start_time
               AND rs.last_execution_time < @history_end_time)
        OR (rs.first_execution_time <= @history_start_time
               AND rs.last_execution_time > @history_start_time)
        OR (rs.first_execution_time <= @history_end_time
               AND rs.last_execution_time > @history_end_time)
    GROUP BY p.query_id
),
recent AS
(
    SELECT
        p.query_id query_id,
        ROUND(ROUND(CONVERT(FLOAT, SUM(rs.avg_duration * rs.count_executions)) * 0.001, 2), 2) AS total_duration,
        SUM(rs.count_executions) AS count_executions,
        COUNT(distinct p.plan_id) AS num_plans
    FROM sys.query_store_runtime_stats AS rs
        JOIN sys.query_store_plan AS p ON p.plan_id = rs.plan_id
    WHERE  (rs.first_execution_time >= @recent_start_time
               AND rs.last_execution_time < @recent_end_time)
        OR (rs.first_execution_time <= @recent_start_time
               AND rs.last_execution_time > @recent_start_time)
        OR (rs.first_execution_time <= @recent_end_time
               AND rs.last_execution_time > @recent_end_time)
    GROUP BY p.query_id
)
SELECT
    results.query_id AS query_id,
    results.query_text AS query_text,
    results.additional_duration_workload AS additional_duration_workload,
    results.total_duration_recent AS total_duration_recent,
    results.total_duration_hist AS total_duration_hist,
    ISNULL(results.count_executions_recent, 0) AS count_executions_recent,
    ISNULL(results.count_executions_hist, 0) AS count_executions_hist
FROM
(
    SELECT
        hist.query_id AS query_id,
        qt.query_sql_text AS query_text,
        ROUND(CONVERT(float, recent.total_duration/
                   recent.count_executions-hist.total_duration/hist.count_executions)
               *(recent.count_executions), 2) AS additional_duration_workload,
        ROUND(recent.total_duration, 2) AS total_duration_recent,
        ROUND(hist.total_duration, 2) AS total_duration_hist,
        recent.count_executions AS count_executions_recent,
        hist.count_executions AS count_executions_hist
    FROM hist
        JOIN recent
            ON hist.query_id = recent.query_id
        JOIN sys.query_store_query AS q
            ON q.query_id = hist.query_id
        JOIN sys.query_store_query_text AS qt
            ON q.query_text_id = qt.query_text_id
) AS results
WHERE additional_duration_workload > 0
ORDER BY additional_duration_workload DESC
OPTION (MERGE JOIN);
```

### <a name="maintaining-query-performance-stability"></a><a name="Stability"></a> Como manter a estabilidade do desempenho da consulta

Para consultas executadas várias vezes, você pode perceber que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa diferentes planos, resultando em diferentes utilizações de recurso e duração. Com o Repositório de Consultas, você pode detectar quando o desempenho da consulta regrediu e determinar o plano ideal dentro de um período de interesse. Em seguida, você pode impor esse plano ideal para execução futura da consulta.

Você também pode identificar desempenho inconsistente de consulta para uma consulta com parâmetros (autoparametrizada ou parametrizada manualmente). Entre diferentes planos, você pode identificar o plano que é rápido e ideal o suficiente para todos ou a maioria dos valores de parâmetro e impor esse plano, mantendo desempenho previsível para o conjunto mais amplo de cenários de usuário.

### <a name="force-a-plan-for-a-query-apply-forcing-policy"></a>Impor um plano para uma consulta (aplicar política de imposição)

Quando um plano é imposto em determinada consulta, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta impor o plano no otimizador. Se a imposição do plano falhar, um XEvent será acionado e o otimizador será instruído a otimizar normalmente.

```sql
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;
```

Ao usar **sp_query_store_force_plan** você só pode impor planos registrados pelo repositório de consultas como um plano para essa consulta. Em outras palavras, os únicos planos disponíveis para uma consulta são aqueles que já foram usados para executar essa consulta enquanto o Repositório de Consultas estava ativo.

#### <a name="a-namectp23-plan-forcing-support-for-fast-forward-and-static-cursors"></a><a name="ctp23"><a/> Planejar forçar suporte para cursores estáticos e de avanço rápido

No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e no Banco de Dados SQL do Azure (todos os modelos de implantação) em diante, o Repositório de Consultas dá suporte à capacidade de impor planos de execução de consulta para cursores estáticos e de avanço rápido de API e [!INCLUDE[tsql](../../includes/tsql-md.md)]. Há suporte para a imposição por meio de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou dos relatórios do Repositório de Consultas do `sp_query_store_force_plan`.

### <a name="remove-plan-forcing-for-a-query"></a>Remover a imposição de plano de uma consulta

Para depender novamente no otimizador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular o plano de consulta ideal, use **sp_query_store_unforce_plan** para cancelar a imposição do plano selecionado para a consulta.

```sql
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;
```

## <a name="see-also"></a>Consulte Também

- [Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)
- [Usar o Repositório de Consultas com OLTP in-memory](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)
- [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md)
- [Como o Repositório de Consultas coleta dados](../../relational-databases/performance/how-query-store-collects-data.md)
- [Procedimentos Armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)
- [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)
- [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)
- [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)
- [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)
- [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)
- [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md)
- [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
