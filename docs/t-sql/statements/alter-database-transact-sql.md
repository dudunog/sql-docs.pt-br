---
title: ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 13ef724e531d55a590ded5bc1c3af8da85375e2b
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111245"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)

Modifica determinadas opções de configuração de um banco de dados.

Este artigo fornece a sintaxe, os argumentos, os comentários, as permissões e os exemplos de qualquer produto SQL que você escolher.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância gerenciada<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-sql-server"></a>Visão geral: SQL Server

No SQL Server, essa instrução modifica um banco de dados ou os arquivos e grupos de arquivos associados ao banco de dados. Adiciona ou remove arquivos e grupos de arquivos de um banco de dados, altera os atributos de um banco de dados ou seus arquivos e grupos de arquivos, altera a ordenação de banco de dados e define opções de banco de dados. Instantâneos de banco de dados não podem ser modificados. Para modificar opções de banco de dados associadas à replicação, use [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).

Devido à sua extensão, a sintaxe ALTER DATABASE está separada em vários artigos.

ALTER DATABASE O artigo atual fornece a sintaxe e as informações relacionadas para alterar o nome e a ordenação de um banco de dados.

[Opções de grupo de arquivos e arquivo de banco de dados ALTER](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) Fornece a sintaxe e informações relacionadas para adicionar e remover arquivos e grupos de arquivos de um banco de dados e para alterar os atributos de arquivos e grupos de arquivos.

[Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) Fornece a sintaxe e informações relacionadas para alterar os atributos de um banco de dados usando as opções SET de ALTER DATABASE.

[Espelhamento de banco de dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) Fornece a sintaxe e informações relacionadas para as opções SET de ALTER DATABASE relacionadas ao espelhamento de banco de dados.

[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md) Fornece a sintaxe e informações relacionadas para as opções [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] de ALTER DATABASE para configurar um banco de dados secundário em uma réplica secundária de um Grupo de Disponibilidade AlwaysOn.

[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) Fornece a sintaxe e informações relacionadas para as opções SET de ALTER DATABASE relacionadas aos níveis de compatibilidade do banco de dados.

[ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) Fornece a sintaxe relacionada às configurações no escopo do banco de dados usadas para as configurações individuais no nível do banco de dados, como comportamentos relacionados à otimização e à execução de consulta.

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- SQL Server Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>
  | SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<file_and_filegroup_options>::=
  <add_or_modify_files>::=
  <filespec>::=
  <add_or_modify_filegroups>::=
  <filegroup_updatability_option>::=

<option_spec>::=
{
  | <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <database_mirroring_option>
  | <date_correlation_optimization_option>
  | <db_encryption_option>
  | <db_state_option>
  | <db_update_option>
  | <db_user_access_option><delayed_durability_option>
  | <external_access_option>
  | <FILESTREAM_options>
  | <HADR_options>
  | <parameterization_option>
  | <query_store_options>
  | <recovery_option>
  | <service_broker_option>
  | <snapshot_option>
  | <sql_option>
  | <termination>
  | <temporal_history_retention>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
}
```

## <a name="arguments"></a>Argumentos

*database_name* É o nome do banco de dados a ser modificado.

> [!NOTE]
> Essa opção não está disponível em um banco de dados independente.

CURRENT **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.

Designa que o banco de dados em uso deve ser alterado.

MODIFY NAME **=** _new_database_name_ Renomeia o banco de dados com o nome especificado como *new_database_name*.

COLLATE *collation_name* Especifica a ordenação do banco de dados. *collation_name* pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se não especificado, ao banco de dados será atribuída a ordenação da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

> [!NOTE]
> A ordenação não poderá ser alterada depois que o banco de dados tiver sido criado em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Durante a criação de bancos de dados com itens diferentes da ordenação padrão, os dados no banco de dados sempre respeitam a ordenação especificada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ao criar um banco de dados independente, as informações do catálogo interno serão mantidas por meio da ordenação padrão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **Latin1_General_100_CI_AS_WS_KS_SC**.

Para saber mais sobre nomes de ordenações Windows e SQL, confira [COLLATE](~/t-sql/statements/collations.md).

**\<delayed_durability_option> ::=** 
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.

Para saber mais, confira [Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).

**\<file_and_filegroup_options>::=** Para obter mais informações, confira as [Opções de arquivo e grupo de arquivos ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

## <a name="remarks"></a>Comentários

Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).

Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).

A instrução `ALTER DATABASE` deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não deve ser permitida em uma transação explícita ou implícita.

O estado de um arquivo de banco de dados (por exemplo, online ou offline) é mantido independentemente do estado do banco de dados. Para obter mais informações, consulte [Estados de arquivo](../../relational-databases/databases/file-states.md). O estado dos arquivos dentro de um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Se um grupo de arquivos estiver offline, qualquer tentativa de acessá-lo por meio de uma instrução SQL falhará com erro. Quando você cria planos de consulta para instruções SELECT, o otimizador de consultas evita índices não clusterizados e exibições indexadas que residam em grupos de arquivos offline. Isso permite que essas instruções tenham êxito. Porém, se o grupo de arquivos offline contiver o heap ou índice clusterizado da tabela de destino, as instruções SELECT falharão. Além disso, qualquer instrução `INSERT`, `UPDATE` ou `DELETE` que modifica uma tabela com um índice em um grupo de arquivos offline falhará.

Quando um banco de dados estiver em estado RESTORING, a maioria das instruções `ALTER DATABASE` falhará. A exceção está definindo opções de espelhamento de banco de dados. Um banco de dados pode estar no estado RESTORING durante uma operação de restauração ativa ou quando uma operação de restauração de um banco de dados ou arquivo de log falhar devido a um arquivo de backup corrompido.

O cache do plano para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é limpo pela configuração de uma das seguintes opções.

- COLLATE
- MODIFY FILEGROUP DEFAULT
- MODIFY FILEGROUP READ_ONLY
- MODIFY FILEGROUP READ_WRITE
- MODIFY_NAME
- OFFLINE
- ONLINE
- PAGE_VERIFY
- READ_ONLY
- READ_WRITE

A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`. Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

O cache de planos também é liberado nos seguintes cenários:

- Um banco de dados tem a opção de banco de dados `AUTO_CLOSE` definida como ON. Quando nenhuma conexão de usuário fizer referência ou usar o banco de dados, a tarefa de banco de dados tentará fechar e encerrar o banco de dados automaticamente.
- Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.
- Um instantâneo de banco de dados para um banco de dados de origem é removido.
- Você recria com sucesso o log de transação para um banco de dados.
- Você restaura um backup de banco de dados.
- Você desanexa um banco de dados.

## <a name="changing-the-database-collation"></a>Alterando a ordenação de banco de dados

Antes de aplicar uma ordenação diferente a um banco de dados, certifique-se de que existam as seguintes condições:

- Você é o único usuário que está utilizando o banco de dados no momento.
- Nenhum objeto associado ao esquema depende da ordenação do banco de dados.

Se os objetos a seguir, que dependem da ordenação de banco de dados, existirem no banco de dados, a instrução ALTER DATABASE*database_name*COLLATE falhará. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro para cada objeto que bloqueia a ação de `ALTER`:

- Funções definidas pelo usuário e exibições criadas com SCHEMABINDING
- Colunas computadas
- Restrições CHECK
- Funções com valor de tabela que retornam tabelas com colunas de caracteres com ordenações herdadas da ordenação de banco de dados padrão
  
Informações de dependência de entidades não associadas a esquema são automaticamente atualizadas quando a ordenação de banco de dados é alterada.

Alterar a ordenação de banco de dados não cria duplicatas entre nenhum nome de sistema para os objetos de banco de dados. Se nomes duplicados resultarem da ordenação alterada, os namespaces a seguir poderão provocar falha de alteração de ordenação de banco de dados:

- Nomes de objeto, como procedimentos, tabelas, gatilhos ou exibições
- Nomes de esquema
- Entidades, como grupos, funções ou usuários
- Nomes escalares, como tipos de sistema e tipos definidos pelo usuário
- Nomes de catálogo de texto completo
- Nomes de coluna ou parâmetro dentro de um objeto
- Nomes de índice dentro de uma tabela

Nomes duplicados resultantes da nova ordenação provocarão falha na ação de alteração e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro especificando o namespace onde a duplicata foi encontrada.

## <a name="viewing-database-information"></a>Exibindo informações do banco de dados

É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.

## <a name="permissions"></a>Permissões

Requer a permissão `ALTER` no banco de dados.

## <a name="examples"></a>Exemplos

### <a name="a-changing-the-name-of-a-database"></a>a. Alterando o nome de um banco de dados

O exemplo a seguir altera o nome do banco de dados `AdventureWorks2012` para `Northwind`.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
Modify Name = Northwind ;
GO
```

### <a name="b-changing-the-collation-of-a-database"></a>B. Alterando a ordenação de um banco de dados

O exemplo a seguir cria um banco de dados denominado `testdb` com a ordenação `SQL_Latin1_General_CP1_CI_A`S e, em seguida, altera a ordenação do banco de dados `testdb` para `COLLATE French_CI_AI`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
USE master;
GO

CREATE DATABASE testdb
COLLATE SQL_Latin1_General_CP1_CI_AS ;
GO

ALTER DATABASE testDB
COLLATE French_CI_AI ;
GO
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_Banco de dados individual/pool elástico do \*Banco de Dados SQL<br /> \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Instância gerenciada<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-azure-sql-database-single-databaseelastic-pool"></a>Visão geral: Banco de dados individual/pool elástico do Banco de Dados SQL do Azure

No Banco de Dados SQL do Azure, use essa instrução para modificar um banco de dados em um banco de dados individual/pool elástico. Use esta instrução para alterar o nome de um banco de dados, alterar o objetivo de serviço e a edição do banco de dados, ingressar ou remover o banco de dados para ou de um pool elástico, definir as opções de banco de dados, adicionar ou remover o banco de dados como um secundário em uma relação de replicação geográfica e definir o nível de compatibilidade do banco de dados.

Devido à sua extensão, a sintaxe ALTER DATABASE está separada em vários artigos.

ALTER DATABASE O artigo atual fornece a sintaxe e as informações relacionadas para alterar o nome e a ordenação de um banco de dados.

[Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md?view=azuresqldb-currentls) Fornece a sintaxe e informações relacionadas para alterar os atributos de um banco de dados usando as opções SET de ALTER DATABASE.

[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?view=azuresqldb-currentls) Fornece a sintaxe e informações relacionadas para as opções SET de ALTER DATABASE relacionadas aos níveis de compatibilidade do banco de dados.

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Azure SQL Database Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | MODIFY ( <edition_options> [, ... n] )
  | SET { <option_spec> [ ,... n ] WITH <termination>}
  | ADD SECONDARY ON SERVER <partner_server_name>
    [WITH ( <add-secondary-option>::=[, ... n] ) ]
  | REMOVE SECONDARY ON SERVER <partner_server_name>
  | FAILOVER
  | FORCE_FAILOVER_ALLOW_DATA_LOSS
}
[;]

<edition_options> ::=
{

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }
  | EDITION = { 'Basic' | 'Standard' | 'Premium' | 'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale'}
  | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) }
       }
}

<add-secondary-option> ::=
   {
      ALLOW_CONNECTIONS = { ALL | NO }
     | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL ( name = <elastic_pool_name>) }
       }
   }

<service-objective> ::={ 'Basic' |'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_Gen4_1' | 'GP_Gen4_2' | 'GP_Gen4_3' | 'GP_Gen4_4' | 'GP_Gen4_5' | 'GP_Gen4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'GP_Fsv2_8' | 'GP_Fsv2_10' | 'GP_Fsv2_12' | 'GP_Fsv2_14' | 'GP_Fsv2_16' | 'GP_Fsv2_18'
      | 'GP_Fsv2_20' | 'GP_Fsv2_24' | 'GP_Fsv2_32' | 'GP_Fsv2_36' | 'GP_Fsv2_72'
      | 'GP_S_Gen5_1' | 'GP_S_Gen5_2' | 'GP_S_Gen5_4' | 'GP_S_Gen5_6' | 'GP_S_Gen5_8'
      | 'GP_S_Gen5_10' | 'GP_S_Gen5_12' | 'GP_S_Gen5_14' | 'GP_S_Gen5_16'
      | 'GP_S_Gen5_18' | 'GP_S_Gen5_20' | 'GP_S_Gen5_24' | 'GP_S_Gen5_32' | 'GP_S_Gen5_40'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'BC_M_8' | 'BC_M_10' | 'BC_M_12' | 'BC_M_14' | 'BC_M_16' | 'BC_M_18'
      | 'BC_M_20' | 'BC_M_24' | 'BC_M_32' | 'BC_M_64' | 'BC_M_128'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) }
      }

<option_spec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
  | <compatibility_level>
    { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}
```

## <a name="arguments"></a>Argumentos

*database_name* É o nome do banco de dados a ser modificado.

CURRENT Designa que o banco de dados em uso deve ser alterado.

MODIFY NAME **=** _new_database_name_ Renomeia o banco de dados com o nome especificado como *new_database_name*. O exemplo a seguir altera o nome de um banco de dados `db1` para `db2`:

```sql
ALTER DATABASE db1
    MODIFY Name = db2 ;
```

MODIFY (EDITION **=** ['Basic' | 'Standard' | 'Premium' |'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale']) Altera a camada de serviço do banco de dados.

O exemplo a seguir altera a edição para `Premium`:

```sql
ALTER DATABASE current
    MODIFY (EDITION = 'Premium');
```

> [!IMPORTANT]
> A alteração da edição falhará se a propriedade MAXSIZE do banco de dados estiver definida como um valor fora do intervalo válido compatível com essa edição.

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024...4096] GB) Especifica o tamanho máximo do banco de dados. O tamanho máximo deve estar em conformidade com o conjunto válido de valores da propriedade EDITION do banco de dados. A alteração do tamanho máximo do banco de dados pode fazer com que a EDIÇÃO do banco de dados seja alterada.

> [!NOTE]
> O argumento **MAXSIZE** não é aplicável a bancos de dados individuais na camada de serviço em hiperescala. Os bancos de dados da camada de serviço em hiperescala crescem conforme necessário até 100 TB. O serviço de Banco de Dados SQL adiciona armazenamento automaticamente – não é necessário definir um tamanho máximo.

**Modelo da DTU**

|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|
|100 MB|√|√|√|√|√|
|250 MB|√|√|√|√|√|
|500 MB|√|√|√|√|√|
|1 GB|√|√|√|√|√|
|2 GB|√ (D)|√|√|√|√|
|5 GB|N/D|√|√|√|√|
|10 GB|N/D|√|√|√|√|
|20 GB|N/D|√|√|√|√|
|30 GB|N/D|√|√|√|√|
|40 GB|N/D|√|√|√|√|
|50 GB|N/D|√|√|√|√|
|100 GB|N/D|√|√|√|√|
|150 GB|N/D|√|√|√|√|
|200 GB|N/D|√|√|√|√|
|250 GB|N/D|√ (D)|√ (D)|√|√|
|300 GB|N/D|√|√|√|√|
|400 GB|N/D|√|√|√|√|
|500 GB|N/D|√|√|√ (D)|√|
|750 GB|N/D|√|√|√|√|
|1024 GB|N/D|√|√|√|√ (D)|
|De 1024 GB até 4096 GB em incrementos de 256 GB*|N/D|N/D|N/D|N/D|√|

\* P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB sendo o tamanho padrão. P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, um MAXSIZE maior que 1 TB está atualmente disponível nas seguintes regiões: Leste dos EUA 2, Oeste dos EUA, US Gov – Virgínia, Europa Ocidental, Região Central da Alemanha, Sudeste da Ásia, Leste do Japão, Leste da Austrália, Região Central do Canadá e Leste do Canadá. Para obter detalhes adicionais sobre limitações de recursos para o modelo de DTU, veja [Limites de recurso de DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).

O valor MAXSIZE do modelo de DTU, se especificado, deve ser um valor válido exibido na tabela acima para a camada de serviço especificada.

**modelo vCore**

**Uso Geral – computação provisionada – Gen4 (parte 1)**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|

**Uso Geral – computação provisionada – Gen4 (parte 2)**

|MAXSIZE|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|Tamanho máximo de dados (GB)|1536|3072|3072|3072|4096|4096|

**Uso Geral – computação provisionada – Gen5 (parte 1)**

|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|1536|

**Uso Geral – computação provisionada – Gen5 (parte 2)**

|MAXSIZE|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|3072|3072|3072|4096|4096|4096|4096|

**Uso Geral – computação provisionada – série Fsv2 (parte 1)**

|MAXSIZE|GP_Fsv2_8|GP_Fsv2_10|GP_Fsv2_12|GP_Fsv2_14|GP_Fsv2_16|GP_Fsv2_18|
|:----- | ------: | ------: | ------: | ------: | ------: | ------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1536|1536|

**Uso Geral – computação provisionada – série Fsv2 (parte 2)**

|MAXSIZE|GP_Fsv2_20|GP_Fsv2_24|GP_Fsv2_32|GP_Fsv2_36|GP_Fsv2_72|
|:----- | ------: | ------: | ------: | ------: | ------: |
|Tamanho máximo de dados (GB)|1536|1536|3072|3072|4096|

**Uso Geral – computação sem servidor – Gen5 (parte 1)**

|MAXSIZE|GP_S_Gen5_1|GP_S_Gen5_2|GP_S_Gen5_4|GP_S_Gen5_6|GP_S_Gen5_8|
|:----- | ------: |-------: |-------: |-------: |--------: |
|Máximo de vCores|1|2|4|6|8|

**Uso Geral – computação sem servidor – Gen5 (parte 2)**

|MAXSIZE|GP_S_Gen5_10|GP_S_Gen5_12|GP_S_Gen5_14|GP_S_Gen5_16|
|:----- | ------: |-------: |-------: |-------: |
|Máximo de vCores|10|12|14|16|

**Uso Geral – computação sem servidor – Gen5 (parte 3)**

|MAXSIZE|GP_S_Gen5_18|GP_S_Gen5_20|GP_S_Gen5_24|GP_S_Gen5_32|GP_S_Gen5_40|
|:----- | ------: |-------: |-------: |-------: |--------: |
|Máximo de vCores|18|20|24|32|40|

**Comercialmente Crítico – computação provisionada – Gen4 (parte 1)**

|Tamanho da computação (objetivo do serviço)|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--------------- | ------: |-------: |-------: |-------: |-------: |-------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1024|1024|

**Comercialmente Crítico – computação provisionada – Gen4 (parte 2)**

|Tamanho da computação (objetivo do serviço)|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--------------- | ------: |-------: |-------: |--------: |--------: |--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1024|1024|

**Comercialmente Crítico – computação provisionada – Gen5 (parte 1)**

|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |---------: |--------:|--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|1536|

**Comercialmente Crítico – computação provisionada – Gen5 (parte 2)**

|MAXSIZE|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:----- | -------: |--------: |--------: |--------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|3072|3072|3072|4096|4096|4096|4096|

**Comercialmente Crítico – computação provisionada – série M (parte 1)**

|MAXSIZE|BC_M_8|BC_M_10|BC_M_12|BC_M_14|BC_M_16|BC_M_18|
|:----- | -------: | -------: | -------: | -------: | -------: | -------: |
|Tamanho máximo de dados (GB)|512|640|768|896|1024|1152|

**Comercialmente crítico – computação provisionada – série M (parte 2)**

|MAXSIZE|BC_M_20|BC_M_24|BC_M_32|BC_M_64|BC_M_128|
|:----- | -------: | -------: | -------: | -------: | -------: |
|Tamanho máximo de dados (GB)|1280|1536|2\.048|4096|4096|

Se nenhum `MAXSIZE`valor for definido ao usar o modelo vCore, o padrão será de 32 GB. Para obter detalhes adicionais sobre limitações de recursos para o modelo de vCore, confira [Limites de recurso de vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).

As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:

- Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido como Standard e MAXSIZE não for especificado, MAXSIZE será automaticamente definido como 250 MB.
- Se nem MAXSIZE nem EDITION forem especificados, EDITION será definido como Uso Geral e MAXSIZE será definido como 32 GB.

MODIFY (SERVICE_OBJECTIVE = \<service-objective>) Especifica o tamanho da computação (objetivo do serviço). O seguinte exemplo altera o objetivo de serviço de um banco de dados Premium para `P6`:

```sql
ALTER DATABASE current
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```

SERVICE_OBJECTIVE

- **Para bancos de dados individuais e em pool**

  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo de serviço são: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_8`, `GP_Fsv2_10`, `GP_Fsv2_12`, `GP_Fsv2_14`, `GP_Fsv2_16`, `GP_Fsv2_18`, `GP_Fsv2_20`, `GP_Fsv2_24`, `GP_Fsv2_32`, `GP_Fsv2_36`, `GP_Fsv2_72`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`, `BC_Gen5_40`, `BC_Gen5_80`, `BC_M_8`, `BC_M_10`, `BC_M_12`, `BC_M_14`, `BC_M_16`, `BC_M_18`, `BC_M_20`, `BC_M_24`, `BC_M_32`, `BC_M_64`, `BC_M_128`.

- **Para bancos de dados individuais na camada de computação sem servidor**

  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo do serviço são: `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `GP_S_Gen5_18`, `GP_S_Gen5_20`, `GP_S_Gen5_24`, `GP_S_Gen5_32` e `GP_S_Gen5_40`.

- **Para bancos de dados individuais na camada de serviço em hiperescala**

  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo do serviço são: `HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`, `HS_GEN4_24`, `HS_Gen5_2`, `HS_Gen5_4`, `HS_Gen5_8`, `HS_Gen5_16`, `HS_Gen5_24`, `HS_Gen5_32`, `HS_Gen5_48`, `HS_Gen5_80`.

Para obter descrições de objetivos de serviço e mais informações sobre o tamanho, as edições e as combinações de objetivo de serviço, veja [Camadas de serviço e níveis de desempenho do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/), [Limites de recurso de DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) e [Limites de recurso de vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits). O suporte para objetivos de serviço PRS foi removido. Em caso de dúvidas, use este alias de email: premium-rs@microsoft.com.

MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>) Para adicionar um banco de dados existente a um pool elástico, defina o SERVICE_OBJECTIVE do banco de dados como ELASTIC_POOL e forneça o nome do pool elástico. Você também pode usar esta opção para alterar o banco de dados para um pool elástico diferente no mesmo servidor. Para obter mais informações, confira [Criar e gerenciar um pool elástico do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Para remover um banco de dados de um pool elástico, use ALTER DATABASE para definir o SERVICE_OBJECTIVE como um tamanho da computação (objetivo do serviço) de banco de dados individual.

> [!NOTE]
> Bancos de dados na camada de serviço de Hiperescala não podem ser adicionados a um pool elástico.

ADICIONAR SECUNDÁRIO NO SERVIDOR \<partner_server_name>

Cria um banco de dados de replicação geográfica secundário com o mesmo nome em um servidor parceiro, tornando o banco de dados local o primário da replicação geográfica e começa a replicação de dados assíncrona do primário para o novo secundário. Se um banco de dados com o mesmo nome já existir no secundário, o comando falhará. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados local que se torna o primário.

> [!IMPORTANT]
> No momento, a camada de serviço de Hiperescala no momento não dá suporte para replicação geográfica.

WITH ALLOW_CONNECTIONS { **ALL** | NO } Quando ALLOW_CONNECTIONS não for especificado, ele será definido como ALL por padrão. Se estiver definido como ALL, ele será um banco de dados somente leitura que permite que todos os logons com as permissões apropriadas se conectem.

WITH SERVICE_OBJECTIVE { `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_8`, `GP_Fsv2_10`, `GP_Fsv2_12`, `GP_Fsv2_14`, `GP_Fsv2_16`, `GP_Fsv2_18`, `GP_Fsv2_20`, `GP_Fsv2_24`, `GP_Fsv2_32`, `GP_Fsv2_36`, `GP_Fsv2_72`, `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `GP_S_Gen5_18`, `GP_S_Gen5_20`, `GP_S_Gen5_24`, `GP_S_Gen5_32`, `GP_S_Gen5_40`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`, `BC_Gen5_40`, `BC_Gen5_80`, `BC_M_8`, `BC_M_10`, `BC_M_12`, `BC_M_14`, `BC_M_16`, `BC_M_18`, `BC_M_20`, `BC_M_24`, `BC_M_32`, `BC_M_64`, `BC_M_128` }

Quando SERVICE_OBJECTIVE não for especificado, o banco de dados secundário será criado no mesmo nível de serviço que o banco de dados primário. Quando SERVICE_OBJECTIVE for especificado, o banco de dados secundário será criado no nível especificado. Essa opção permite a criação de secundários replicados geograficamente com níveis de serviço mais baratos. O SERVICE_OBJECTIVE especificado precisa estar na mesma edição que a origem. Por exemplo, não é possível especificar S0 se a edição for Premium.

ELASTIC_POOL (name = \<elastic_pool_name>) Quando ELASTIC_POOL não for especificado, o banco de dados secundário não será criado em um pool elástico. Quando ELASTIC_POOL for especificado, o banco de dados secundário será criado no pool especificado.

> [!IMPORTANT]
> O usuário que executa o comando ADD SECONDARY precisa ser DBManager no servidor primário, ter associação a db_owner no banco de dados local e DBManager no servidor secundário.

REMOVE SECONDARY ON SERVER \<partner_server_name> Remove o banco de dados secundário com replicação geográfica especificado do servidor especificado. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados primário.

> [!IMPORTANT]
> O usuário que executa o comando REMOVE SECONDARY precisa ser DBManager no servidor primário.

FAILOVER Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para se tornar o primário e rebaixa o primário atual para se tornar o novo secundário. Como parte desse processo, o modo de replicação geográfica é temporariamente alternado de modo assíncrono para modo síncrono. Durante o processo de failover:

1. O primário deixa de assumir novas transações.
2. Todas as transações pendentes são liberadas para o secundário.
3. O secundário torna-se o primário e inicia a replicação geográfica assíncrona com o antigo primário que agora é o novo secundário.

Esta sequência garante que não haja nenhuma perda de dados. O período durante o qual os dois bancos de dados não estão disponíveis é de 0 a 25 segundos, enquanto as funções são trocadas. A operação total não deve durar mais que cerca de um minuto. Se o banco de dados primário estiver indisponível quando esse comando for emitido, o comando falhará com uma mensagem de erro indicando que o banco de dados primário não está disponível. Se o processo de failover não for concluído e parecer paralisado, você poderá usar o comando para forçar o failover e aceitar a perda de dados. Em seguida, se for necessário recuperar os dados perdidos, chame DevOps (CSS).

> [!IMPORTANT]
> O usuário que executa o comando FAILOVER precisa ser DBManager no servidor primário e no servidor secundário.

FORCE_FAILOVER_ALLOW_DATA_LOSS Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para se tornar o primário e rebaixa o primário atual para se tornar o novo secundário. Use este comando somente quando o primário atual não estiver mais disponível. Ele foi projetado somente para recuperação de desastre, quando a restauração da disponibilidade é crítica e a perda de alguns dados é aceitável.

Durante um failover forçado:

1. O banco de dados secundário especificado torna-se imediatamente o banco de dados primário e começa a aceitar novas transações.
2. Quando o primário original pode se reconectar com o novo primário, um backup incremental é realizado no primário original e ele se torna o novo secundário.
3. Para recuperar dados desse backup incremental no antigo primário, o usuário emprega DevOps/CSS.
4. Se houver outros secundários, eles serão reconfigurados automaticamente para tornarem-se secundários do novo primário. Esse processo é assíncrono e pode haver um atraso até que ele seja concluído. Até que a reconfiguração seja concluída, os secundários continuarão como secundários do antigo primário.

> [!IMPORTANT]
> O usuário que executa o comando `FORCE_FAILOVER_ALLOW_DATA_LOSS` precisa ser `dbmanager` no servidor primário e no servidor secundário.

## <a name="remarks"></a>Comentários

Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).
Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).

A instrução `ALTER DATABASE` deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não deve ser permitida em uma transação explícita ou implícita.

A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`. Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

O cache de procedimento também é liberado no seguinte cenário: Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.

## <a name="viewing-database-information"></a>Exibindo informações do banco de dados

É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.

## <a name="permissions"></a>Permissões

Para alterar um banco de dados, um logon precisa ser o logon da entidade de segurança no nível do servidor (criado pelo processo de provisionamento), um membro da função de banco de dados `dbmanager` no mestre, um membro da função de banco de dados `db_owner` no banco de dados atual ou `dbo` do banco de dados.

## <a name="examples"></a>Exemplos

### <a name="a-check-the-edition-options-and-change-them"></a>a. Verifique as opções de edição e altere-as

Define uma edição e um tamanho máximo para o banco de dados db1:

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Movendo um banco de dados para um pool elástico diferente

Move um banco de dados existente para um pool chamado pool1:

```sql
ALTER DATABASE db1
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;
```

### <a name="c-add-a-geo-replication-secondary"></a>C. Adicionar um secundário de replicação geográfica

Cria o banco de dados secundário legível db1 no servidor `secondaryserver` do db1 no servidor local.

```sql
ALTER DATABASE db1
ADD SECONDARY ON SERVER secondaryserver
WITH ( ALLOW_CONNECTIONS = ALL )
```

### <a name="d-remove-a-geo-replication-secondary"></a>D. Remover um secundário de replicação geográfica

Remove o banco de dados secundário db1 do servidor `secondaryserver`.

```sql
ALTER DATABASE db1
REMOVE SECONDARY ON SERVER testsecondaryserver
```

### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Failover para um secundário de replicação geográfica

Promove o banco de dados secundário db1 no servidor `secondaryserver` para tornar-se o novo banco de dados primário quando executado no servidor `secondaryserver`.

```sql
ALTER DATABASE db1 FAILOVER
```

### <a name="e-force-failover-to-a-geo-replication-secondary-with-data-loss"></a>E. Forçar o failover para um secundário de replicação geográfica com perda de dados

Força um banco de dados secundário db1 no servidor `secondaryserver` a se tornar o novo banco de dados primário quando executado no servidor `secondaryserver`, caso o servidor primário se torne não disponível. Essa opção pode gerar a perda de dados.

```sql
ALTER DATABASE db1 FORCE_FAILOVER_ALLOW_DATA_LOSS
```

### <a name="g-update-a-single-database-to-service-tier-s0-standard-edition-performance-level-0"></a>G. Atualizar um banco de dados individual para a camada de serviço S0 (Edição Standard, nível de desempenho 0)

Atualiza um banco de dados individual para a Edição Standard (camada de serviço) com um tamanho da computação (objetivo do serviço) do S0 e um tamanho máximo de 250 GB.

```sql
ALTER DATABASE [db1] MODIFY (EDITION = 'Standard', MAXSIZE = 250 GB, SERVICE_OBJECTIVE = 'S0');
```

## <a name="see-also"></a>Confira também

- [CREATE DATABASE – Banco de Dados SQL do Azure](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-currentls)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_Instância gerenciada do \*Banco de Dados SQL<br /> \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::



&nbsp;

## <a name="overview-azure-sql-database-managed-instance"></a>Visão geral: Instância gerenciada do Banco de Dados SQL do Azure

Na instância gerenciada de Banco de Dados do SQL, use esta instrução para definir opções de banco de dados.

Devido à sua extensão, a sintaxe ALTER DATABASE está separada em vários artigos.

ALTER DATABASE O artigo atual fornece a sintaxe e as informações relacionadas para definir opções de arquivo e grupo de arquivos, para definir opções de banco de dados e para definir o nível de compatibilidade do banco de dados.  
  
[Opções de grupo de arquivos e arquivo de banco de dados ALTER](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md?&tabs=sqldbmi) Fornece a sintaxe e informações relacionadas para adicionar e remover arquivos e grupos de arquivos de um banco de dados e para alterar os atributos de arquivos e grupos de arquivos.  
  
[Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbmi) Fornece a sintaxe e informações relacionadas para alterar os atributos de um banco de dados usando as opções SET de ALTER DATABASE.  
  
[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbmi) Fornece a sintaxe e informações relacionadas para as opções SET de ALTER DATABASE relacionadas aos níveis de compatibilidade do banco de dados.  

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ]  
}  
[;]

<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  

<option_spec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>  
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <temporal_history_retention>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}  

```

## <a name="arguments"></a>Argumentos

*database_name* É o nome do banco de dados a ser modificado.

CURRENT Designa que o banco de dados em uso deve ser alterado.

## <a name="remarks"></a>Comentários

Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).
Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).

A instrução `ALTER DATABASE` deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não deve ser permitida em uma transação explícita ou implícita.

A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrências de liberação de armazenamento em cache para o armazenamento em cache '%s' (parte do cache de planos) devido a operações de reconfiguração ou manutenção do banco de dados". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

O cache de planos também é liberado quando várias consultas são executadas em um banco de dados que possui opções padrão. O banco de dados é removido.

## <a name="viewing-database-information"></a>Exibindo informações do banco de dados

É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.

## <a name="permissions"></a>Permissões

Somente o logon de entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou os membros da função de banco de dados `dbcreator` podem alterar um banco de dados.

> [!IMPORTANT]
> O proprietário do banco de dados não pode alterar o banco de dados, a menos que seja um membro da função `dbcreator`.

## <a name="examples"></a>Exemplos

Os exemplos a seguir mostram como definir o ajuste automático e como adicionar um arquivo em uma instância gerenciada.

```sql
ALTER DATABASE WideWorldImporters
  SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON)

ALTER DATABASE WideWorldImporters
  ADD FILE (NAME = 'data_17')
```

## <a name="see-also"></a>Confira também

- [CREATE DATABASE – Banco de Dados SQL do Azure](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância gerenciada<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-azure-synapse-analytics"></a>Visão geral: Azure Synapse Analytics

No Azure Synapse, "ALTER DATABASE" modifica o nome, o tamanho máximo ou o objetivo de serviço de um banco de dados.

Devido à sua extensão, a sintaxe ALTER DATABASE está separada em vários artigos.

[Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) Fornece a sintaxe e informações relacionadas para alterar os atributos de um banco de dados usando as opções SET de ALTER DATABASE.

## <a name="syntax"></a>Sintaxe

```console
ALTER DATABASE { database_name | CURRENT }
{
  MODIFY NAME = new_database_name
| MODIFY ( <edition_option> [, ... n] )
| SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<edition_option> ::=
      MAXSIZE = {
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920
          | 92160 | 102400 | 153600 | 204800 | 245760
      } GB
      | SERVICE_OBJECTIVE = {
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500'
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000'
          | 'DW3000' | 'DW6000' | 'DW500c' | 'DW1000c' | 'DW1500c'
          | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c'
          | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }
```

## <a name="arguments"></a>Argumentos

*database_name* Especifica o nome do banco de dados a ser modificado.

MODIFY NAME = *new_database_name* Renomeia o banco de dados com o nome especificado como *new_database_name*.

MAXSIZE O padrão é 245.760 GB (240 TB).

**Aplica-se a:** Otimizado para Computação Gen1

O tamanho máximo permitido para o banco de dados. O banco de dados não pode ultrapassar o MAXSIZE.

**Aplica-se a:** Otimizado para Computação Gen2

O tamanho máximo permitido para dados de rowstore no banco de dados. Os dados armazenados em tabelas rowstore, um deltastore de um índice columstore ou um índice não clusterizado em um índice columnstore clusterizado não podem exceder o MAXSIZE. Os dados compactados no formato columnstore não têm um limite de tamanho e não estão restritos pelo MAXSIZE.

SERVICE_OBJECTIVE Especifica o tamanho da computação (objetivo do serviço). Para saber mais sobre os objetivos de serviço para o Azure Synapse, confira [Unidades de Data Warehouse (DWUs)](https://docs.microsoft.com/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu).

## <a name="permissions"></a>Permissões

Requer estas permissões:

- Logon da entidade de segurança no nível do servidor (aquele criado pelo processo de provisionamento), ou
- Membro da função de banco de dados `dbmanager`.

O proprietário do banco de dados não pode alterar o banco de dados, a menos que ele seja membro da função `dbmanager`.

## <a name="general-remarks"></a>Comentários gerais

O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto você está conectado ao banco de dados mestre**.

Por padrão, o COMPATIBILITY_LEVEL na Análise de SQL é definido como 130 e não pode ser alterado. Para obter mais detalhes, confira [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/) (Melhor desempenho de consulta com o nível de compatibilidade 130 no Banco de Dados SQL do Azure).

> [!NOTE]
> O COMPATIBILITY_LEVEL aplica-se somente a recursos provisionados (pools).

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

Para executar `ALTER DATABASE`, o banco de dados deve estar online e não pode estar no estado de pausa.

A instrução `ALTER DATABASE` precisa ser executada no modo de confirmação automática, que é o modo padrão de gerenciamento de transações. Isso é definido nas configurações de conexão.

A instrução `ALTER DATABASE` não pode fazer parte de uma transação definida pelo usuário.

Você não pode alterar a ordenação de banco de dados.

## <a name="examples"></a>Exemplos

Antes de executar esses exemplos, verifique se o banco de dados que você está alterando não é o banco de dados atual. O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto você está conectado ao banco de dados mestre**.

### <a name="a-change-the-name-of-the-database"></a>a. Alterar o nome do banco de dados

```sql
ALTER DATABASE AdventureWorks2012
MODIFY NAME = Northwind;
```

### <a name="b-change-max-size-for-the-database"></a>B. Alterar o tamanho máximo do banco de dados

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );
```

### <a name="c-change-the-compute-size-service-objective"></a>C. Alterar o tamanho da computação (objetivo do serviço)

```sql
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );
```

### <a name="d-change-the-max-size-and-the-compute-size-service-objective"></a>D. Alterar o tamanho máximo e o tamanho da computação (objetivo do serviço)

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE (Azure Synapse Analytics)](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [Lista de artigos de referência do Azure Synapse Analytics](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-reference/)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância gerenciada<br />do Banco de Dados SQL](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System (PDW) \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-analytics-platform-system"></a>Visão geral: Sistema de plataforma de análise

Modifica as opções de tamanho máximo do banco de dados para tabelas replicadas, tabelas distribuídas e para o log de transações no PDW. Use esta instrução para gerenciar as alocações de espaço em disco para um banco de dados à medida que ele aumenta ou diminui de tamanho. O artigo também descreve a sintaxe relacionada à configuração das opções de banco de dados no PDW.

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Analytics Platform System
ALTER DATABASE database_name
    SET ( <set_database_options> | <db_encryption_option> )
[;]

<set_database_options> ::=
{
    AUTOGROW = { ON | OFF }
    | REPLICATED_SIZE = size [GB]
    | DISTRIBUTED_SIZE = size [GB]
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<db_encryption_option> ::=
    ENCRYPTION { ON | OFF }
```

## <a name="arguments"></a>Argumentos

*database_name* O nome do banco de dados a ser modificado. Para exibir uma lista de bancos de dados no dispositivo, use [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

AUTOGROW = { ON | OFF } Atualiza a opção AUTOGROW. Quando AUTOGROW for ON, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] aumentará automaticamente o espaço alocado para tabelas replicadas, tabelas distribuídas e log de transações, conforme o necessário, para acomodar o crescimento dos requisitos de armazenamento. Quando o crescimento automático for OFF, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] retornará um erro se as tabelas, replicadas, as tabelas distribuída ou o log de transações exceder o tamanho máximo.

REPLICATED_SIZE = *size* [GB] Especifica o novo máximo de gigabytes por nó de computação para armazenar todas as tabelas replicadas no banco de dados que está sendo alterado. Se você estiver planejando o espaço de armazenamento do dispositivo, multiplique REPLICATED_SIZE pelo número de nós de computação no dispositivo.

DISTRIBUTED_SIZE = *size* [GB] Especifica o novo máximo de gigabytes por banco de dados para armazenar todas as tabelas distribuídas no banco de dados que está sendo alterado. O tamanho é distribuído entre todos os nós de computação no dispositivo.

LOG_SIZE = *size* [GB] Especifica o novo máximo de gigabytes por banco de dados para armazenar todos os logs de transações no banco de dados que está sendo alterado. O tamanho é distribuído entre todos os nós de computação no dispositivo.

ENCRYPTION { ON | OFF } Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). A criptografia poderá ser configurada para o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] somente quando [sp_pdw_database_encryption](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md) tiver sido definido como **1**. Uma chave de criptografia do banco de dados precisa ser criada para que a Transparent Data Encryption possa ser configurada. Para obter mais informações sobre a criptografia do banco de dados, confira [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md).

SET AUTO_CREATE_STATISTICS { ON | OFF } Quando a opção de criação automática de estatísticas, AUTO_CREATE_STATISTICS, está ativada, o otimizador de consulta cria estatísticas em colunas individuais no predicado da consulta, conforme necessário, a fim de melhorar as estimativas de cardinalidade do plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um histograma em um objeto de estatísticas existente.

O padrão é ATIVADO para novos bancos de dados criados após a atualização para o AU7. O padrão é DESATIVADO para bancos de dados criados antes da atualização.

Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md)

SET AUTO_UPDATE_STATISTICS { ON | OFF } Quando a opção de atualização automática de estatísticas, AUTO_UPDATE_STATISTICS, está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição dos dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.

O padrão é ATIVADO para novos bancos de dados criados após a atualização para o AU7. O padrão é DESATIVADO para bancos de dados criados antes da atualização.

Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md).

SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } A opção de atualização de estatísticas assíncrona, AUTO_UPDATE_STATISTICS_ASYNC, determina se o Otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução CREATE STATISTICS.

O padrão é ATIVADO para novos bancos de dados criados após a atualização para o AU7. O padrão é DESATIVADO para bancos de dados criados antes da atualização.

Para obter mais informações sobre estatísticas, consulte [Estatísticas](/sql/relational-databases/statistics/statistics).

## <a name="permissions"></a>Permissões

Requer a permissão `ALTER` no banco de dados.

## <a name="error-messages"></a>Mensagens de erro

Se as estatísticas automáticas estiverem habilitadas e você tentar alterar as configurações delas, o PDW apresentará o erro `This option is not supported in PDW`. O administrador do sistema pode habilitar estatísticas automáticas, permitindo a opção de recurso [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md).

## <a name="general-remarks"></a>Comentários gerais

Os valores de `REPLICATED_SIZE`,`DISTRIBUTED_SIZE` e `LOG_SIZE` podem ser maiores, iguais ou menores que os valores atuais do banco de dados.

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

As operações de crescimento e redução são aproximadas. Os tamanhos reais resultantes podem variar em relação aos parâmetros de tamanho.

O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não executa a instrução ALTER DATABASE como uma operação atômica. Se a instrução for anulada durante a execução, as alterações já feitas permanecerão.

As configurações de estatísticas só funcionarão se o administrador habilitar estatísticas automáticas. Se você for administrador, use a opção de recurso [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) para habilitar ou desabilitar estatísticas automáticas.

## <a name="locking-behavior"></a>Comportamento de bloqueio

Usa um bloqueio compartilhado no objeto DATABASE. Não é possível alterar um banco de dados que esteja sendo usado por outro usuário para leitura ou gravação. Isso inclui as sessões que emitiram uma instrução [USE](../language-elements/use-transact-sql.md) no banco de dados.

## <a name="performance"></a>Desempenho

A redução de um banco de dados pode demorar bastante e usar uma grande quantidade de recursos do sistema, dependendo do tamanho dos dados reais no banco de dados e da quantidade de fragmentação no disco. Por exemplo, a redução de um banco de dados pode levar várias horas ou mais.

## <a name="determining-encryption-progress"></a>Determinando o andamento da criptografia

Use a consulta a seguir para determinar o andamento da Transparent Data Encryption do banco de dados como um percentual:

```sql
WITH
database_dek AS (
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,
        dek.encryption_state, dek.percent_complete,
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,
        type
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map
        ON dek.database_id = node_db_map.database_id
        AND dek.pdw_node_id = node_db_map.pdw_node_id
    LEFT JOIN sys.pdw_database_mappings AS db_map
        ON node_db_map .physical_name = db_map.physical_name
    INNER JOIN sys.dm_pdw_nodes nodes
        ON nodes.pdw_node_id = dek.pdw_node_id
    WHERE dek.encryptor_thumbprint <> 0x
),
dek_percent_complete AS (
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete
    FROM database_dek
    WHERE type = 'COMPUTE'
    GROUP BY database_dek.database_id
)
SELECT DB_NAME( database_dek.database_id ) AS name,
    database_dek.database_id,
    ISNULL(
       (SELECT TOP 1 dek_encryption_state.encryption_state
        FROM database_dek AS dek_encryption_state
        WHERE dek_encryption_state.database_id = database_dek.database_id
        ORDER BY (CASE encryption_state
            WHEN 3 THEN -1
            ELSE encryption_state
            END) DESC), 0)
        AS encryption_state,
dek_percent_complete.percent_complete,
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint
FROM database_dek
INNER JOIN dek_percent_complete
    ON dek_percent_complete.database_id = database_dek.database_id
WHERE type = 'CONTROL';
```

Para obter um exemplo abrangente que demonstra todas as etapas da implementação de TDE, confira [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md).

## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="a-altering-the-autogrow-setting"></a>a. Alterando a configuração AUTOGROW

Defina AUTOGROW como ON para o banco de dados `CustomerSales`.

```sql
ALTER DATABASE CustomerSales
    SET ( AUTOGROW = ON );
```

### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Alterando o armazenamento máximo para tabelas replicadas

O exemplo a seguir define o limite de armazenamento de tabela replicada em 1 GB para o banco de dados `CustomerSales`. Este é o limite de armazenamento por nó de computação.

```sql
ALTER DATABASE CustomerSales
    SET ( REPLICATED_SIZE = 1 GB );
```

### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Alterando o armazenamento máximo para tabelas distribuídas

 O exemplo a seguir define o limite de armazenamento de tabela distribuída para 1000 GB (um terabyte) para o banco de dados `CustomerSales`. Este é o limite de armazenamento combinado no dispositivo para todos os nós de computação, não o limite de armazenamento por nó de computação.

```sql
ALTER DATABASE CustomerSales
    SET ( DISTRIBUTED_SIZE = 1000 GB );
```

### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Alterando o armazenamento máximo para o log de transações

 O exemplo a seguir atualiza o banco de dados `CustomerSales` para que o tamanho máximo do log de transações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja de 10 GB para o dispositivo.

```sql
ALTER DATABASE CustomerSales
    SET ( LOG_SIZE = 10 GB );
```

### <a name="e-check-for-current-statistics-values"></a>E. Verificar valores atuais de estatísticas

A consulta a seguir retorna os valores atuais de estatísticas para todos os bancos de dados. O valor 1 significa que o recurso está ativado, e 0 significa o recurso está desativado.

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```

### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. Habilitar criação automática e atualização automática de estatísticas para um banco de dados

Use a instrução a seguir para habilitar a criação e atualização de estatísticas automaticamente e de maneira assíncrona para o banco de dados, CustomerSales. Isso cria e atualiza estatísticas de coluna única conforme necessário para criar planos de consulta de alta qualidade.

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON;
ALTER DATABASE
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE – Analytics Platform System](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
