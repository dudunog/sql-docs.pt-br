---
description: CREATE INDEX (Transact-SQL)
title: CREATE INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
author: pmasl
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a31193dfd6d2e29bb5f318ea1b8d70d82d309a8c
ms.sourcegitcommit: 3efd8bbf91f4f78dce3a4ac03348037d8c720e6a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91024497"
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Cria um índice relacional em uma tabela ou exibição. Também chamado de um índice rowstore porque é um índice de árvore B clusterizado ou não clusterizado. Você pode criar um índice rowstore antes que haja dados na tabela. Use um índice rowstore para melhorar o desempenho de consulta, especialmente quando as consultas forem selecionadas de colunas específicas ou exigirem que os valores sejam classificados em uma ordem específica.

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] atualmente não são compatíveis com restrições Exclusivas. Quaisquer exemplos fazendo referência a Restrições Exclusivas são aplicáveis somente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
> [!TIP]
> Para obter informações sobre as diretrizes de design de índice, confira o [Guia de design de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

 **Exemplos simples:**

```sql
-- Create a nonclustered index on a table or view
CREATE INDEX i1 ON t1 (col1);

-- Create a clustered index on a table and use a 3-part name for the table
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);

-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint
-- on 3 columns and specify the sort order for each column
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);
```

**Cenário principal:**

Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], use um índice não clusterizado em um índice columnstore para melhorar o desempenho da consulta de armazenamento de dados. Para obter mais informações, veja [Índices Columnstore – data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md).

Para ver tipos de índices adicionais, consulte:

- [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md)
- [CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md)
- [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md)

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

### <a name="syntax-for-sql-server-and-azure-sql-database"></a>Sintaxe do SQL Server e do Banco de Dados SQL do Azure

```syntaxsql
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )
    [ INCLUDE ( column_name [ ,...n ] ) ]
    [ WHERE <filter_predicate> ]
    [ WITH ( <relational_index_option> [ ,...n ] ) ]
    [ ON { partition_scheme_name ( column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
[ ; ]
  
<object> ::=
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }

<relational_index_option> ::=
{
    PAD_INDEX = { ON | OFF }
  | FILLFACTOR = fillfactor
  | SORT_IN_TEMPDB = { ON | OFF }
  | IGNORE_DUP_KEY = { ON | OFF }
  | STATISTICS_NORECOMPUTE = { ON | OFF }
  | STATISTICS_INCREMENTAL = { ON | OFF }
  | DROP_EXISTING = { ON | OFF }
  | ONLINE = { ON | OFF }
  | RESUMABLE = { ON | OFF }
  | MAX_DURATION = <time> [MINUTES]
  | ALLOW_ROW_LOCKS = { ON | OFF }
  | ALLOW_PAGE_LOCKS = { ON | OFF }
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
  | MAXDOP = max_degree_of_parallelism
  | DATA_COMPRESSION = { NONE | ROW | PAGE }
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }
     [ , ...n ] ) ]
}

<filter_predicate> ::=
    <conjunct> [ AND <conjunct> ]

<conjunct> ::=
    <disjunct> | <comparison>

<disjunct> ::=
        column_name IN (constant ,...n)

<comparison> ::=
        column_name <comparison_op> constant

<comparison_op> ::=
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }

<range> ::=
<partition_number_expression> TO <partition_number_expression>
```

### <a name="backward-compatible-relational-index"></a>Índice relacional compatível com versões anteriores

> [!IMPORTANT]
> A estrutura de sintaxe de índice relacional compatível com versões anteriores será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
> Evite usar essa estrutura de sintaxe em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que a utilizam atualmente.
> Use a estrutura de sintaxe especificada em <relational_index_option>.

```syntaxsql
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )
    [ WITH <backward_compatible_index_option> [ ,...n ] ]
    [ ON { filegroup_name | "default" } ]

<object> ::=
{
    [ database_name. [ owner_name ] . | owner_name. ]
    table_or_view_name
}

<backward_compatible_index_option> ::=
{
    PAD_INDEX
  | FILLFACTOR = fillfactor
  | SORT_IN_TEMPDB
  | IGNORE_DUP_KEY
  | STATISTICS_NORECOMPUTE
  | DROP_EXISTING
}
```

### <a name="syntax-for-azure-synapse-analytics-and-parallel-data-warehouse"></a>Sintaxe do Azure Synapse Analytics e do Parallel Data Warehouse

```syntaxsql

CREATE CLUSTERED COLUMNSTORE INDEX INDEX index_name
    ON [ database_name . [ schema ] . | schema . ] table_name
    [ORDER (column[,...n])]
    [WITH ( DROP_EXISTING = { ON | OFF } )]
[;]


CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON [ database_name . [ schema ] . | schema . ] table_name
        ( { column [ ASC | DESC ] } [ ,...n ] )
    WITH ( DROP_EXISTING = { ON | OFF } )
[;]


```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

UNIQUE      
Cria um índice exclusivo em uma tabela ou exibição. Um índice exclusivo é aquele no qual duas linhas não podem ter o mesmo valor de chave de índice. Um índice clusterizado em uma exibição deve ser exclusivo.

O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não permite a criação de um índice exclusivo em colunas que já contêm valores duplicados, independentemente de IGNORE_DUP_KEY estar definido como ON. Se isso for tentado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibirá uma mensagem de erro. Valores duplicados devem ser removidos para que um índice exclusivo possa ser criado em uma ou mais colunas. As colunas usadas em um índice exclusivo devem ser definidas como NOT NULL, pois vários valores nulos serão considerados duplicatas quando um índice exclusivo for criado.

CLUSTERED      
Cria um índice no qual a ordem lógica dos valores de chave determina a ordem física das linhas correspondentes em uma tabela. O nível inferior, ou folha, do índice clusterizado contém as linhas de dados reais da tabela. Uma tabela ou exibição pode ter um índice clusterizado por vez.

Uma exibição com um índice clusterizado exclusivo é chamada de exibição indexada. Criar um índice clusterizado exclusivo em uma exibição materializa fisicamente a exibição. Um índice clusterizado exclusivo deve ser criado em uma exibição para que qualquer outro índice possa ser definido na mesma exibição. Para obter mais informações, veja [Criar exibições indexadas](../../relational-databases/views/create-indexed-views.md).

Crie o índice clusterizado antes de criar quaisquer índices não clusterizados. Os índices não clusterizados existentes nas tabelas serão recriados quando um índice clusterizado for criado.

Se `CLUSTERED` não for especificado, um índice não clusterizado será criado.

> [!NOTE]
> Uma vez que o nível folha de um índice clusterizado e as páginas de dados são os mesmos por definição, criar um índice clusterizado e usar a cláusula ON *partition_scheme_name* ou ON *filegroup_name* efetivamente move uma tabela do grupo de arquivos em que a tabela foi criada para o novo esquema de partição ou grupo de arquivos. Antes de criar tabelas ou índices em grupos de arquivos específicos, verifique quais grupos de arquivos estão disponíveis e se eles têm espaço vazio suficiente para o índice.

Em alguns casos, criar um novo índice clusterizado pode habilitar índices previamente desabilitados. Para obter mais informações, veja [Habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md) e [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).

NONCLUSTERED      
Cria um índice que especifica a ordem lógica de uma tabela. Com um índice não clusterizado, a ordem física das linhas de dados é independente de sua ordem indexada.

Cada tabela pode ter até 999 índices não clusterizados, independentemente de como eles são criados: seja implicitamente com as restrições PRIMARY KEY e UNIQUE ou explicitamente com CREATE INDEX.

Para exibições indexadas, os índices não clusterizados podem ser criados somente em uma exibição que tenha um índice clusterizado exclusivo já definido.

Se não for especificado de outra forma, o tipo de índice padrão será NONCLUSTERED.

*index_name*      
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela ou exibição, mas não precisam ser exclusivos no banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).

*column*      
 É a coluna, ou colunas, em que o índice se baseia. Especifique dois ou mais nomes de coluna para criar um índice composto com os valores combinados das colunas especificadas. Liste as colunas que serão incluídas no índice composto, em ordem de prioridade de classificação, entre parênteses depois de *table_or_view_name*.

Até 32 colunas podem ser combinadas em uma única chave de índice composto. Todas as colunas de uma chave de índice composto devem estar na mesma tabela ou exibição. O tamanho máximo permitido de valores de índice combinados é de 900 bytes para um índice clusterizado ou de 1.700 para um índice não clusterizado. Os limites são 16 colunas e 900 bytespara versões anteriores a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].

Colunas que são dos tipos de dados LOB (Objeto Grande) **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, ou **image** não podem ser especificadas como colunas chave para um índice. Além disso, uma definição de exibição não pode incluir colunas **ntext**, **text** ou **image**, mesmo que elas não sejam referenciadas na instrução CREATE INDEX.

É possível criar índices em colunas do tipo CLR definido pelo usuário se o tipo der suporte à ordenação binária. Também é possível criar índices em colunas computadas definidas como invocações de método de uma coluna de tipo definido pelo usuário, desde que os métodos sejam marcados como determinísticos e não executem operações de acesso aos dados. Para obter mais informações sobre como indexar colunas CLR de tipo definido pelo usuário, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).

[ **ASC** | DESC ]      
Determina a direção de classificação crescente ou decrescente da coluna de índice específica. O padrão é ASC.

INCLUDE **(** _column_ [ **,** ... *n* ] **)**       
Especifica as colunas não chave a serem adicionadas ao nível folha do índice não clusterizado. O índice não clusterizado pode ser exclusivo ou não exclusivo.

Os nomes de coluna não podem ser repetidos na lista INCLUDE e não podem ser usados simultaneamente como colunas de chave e não chave. Índices não clusterizados sempre conterão as colunas de índice clusterizado se um índice clusterizado for definido na tabela. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).

São permitidos todos os tipos de dados, exceto **text**, **ntext**e **image**. O índice deverá ser criado ou recriado offline (ONLINE = OFF) se qualquer uma das colunas não chave especificadas for dos tipos de dados **varchar(max)** , **nvarchar(max)** ou **varbinary(max)** .

As colunas computadas que são determinísticas e precisas ou imprecisas podem ser colunas incluídas. Colunas computadas derivadas dos tipos de dados **image**, **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e **xml** podem ser incluídas em colunas não chave, desde que os tipos de dados da coluna computada sejam permitidos como uma coluna incluída. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).

Para obter informações sobre como criar um índice XML, veja [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md).

WHERE \<filter_predicate>      
Cria um índice filtrado especificando quais linhas serão incluídas nele. O índice filtrado deve ser um índice não clusterizado em uma tabela. Cria estatísticas filtradas para as linhas de dados no índice filtrado.

O predicado de filtro usa a lógica de comparação simples e não pode fazer referência a uma coluna computada, a uma coluna UDT, a uma coluna de tipo de dados espacial ou a uma coluna de tipo de dados hierarchyID. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.

Estes são alguns exemplos de predicados de filtro da tabela `Production.BillOfMaterials`:

```sql
WHERE StartDate > '20000101' AND EndDate <= '20000630'

WHERE ComponentID IN (533, 324, 753)

WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL
```

Índices filtrados não se aplicam a índices XML e índices de texto completo. Para índices UNIQUE, somente as linhas selecionadas devem ter valores de índice exclusivo. Índices filtrados não permitem a opção IGNORE_DUP_KEY.

ON *partition_scheme_name* **( _column_name_ )**      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica o esquema de partição que define os grupos de arquivos nos quais as partições de um índice particionado serão mapeadas. O esquema de partição deve existir no banco de dados com a execução de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) ou [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *column_name* especifica a coluna com relação à qual um índice particionado será particionado. Essa coluna precisa corresponder ao tipo de dados, ao comprimento e à precisão do argumento da função de partição que *partition_scheme_name* está usando. *column_name* não é restrito às colunas na definição de índice. Qualquer coluna da tabela base pode ser especificada, exceto que, ao particionar um índice UNIQUE, *column_name* deve ser escolhido entre aqueles usados como chave exclusiva. Essa restrição permite ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificar a exclusividade de valores de chave em uma única partição apenas.

> [!NOTE]
> Ao particionar um índice clusterizado não exclusivo, por padrão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento à lista de chaves de índices clusterizados, se ela já não estiver especificada. Ao particionar um índice não clusterizado e não exclusivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento como uma coluna não chave (incluída) do índice, se ela já não estiver especificada.

Se _partition_scheme_name_ ou _filegroup_ não for especificado e a tabela estiver particionada, o índice será colocado no mesmo esquema de partição, usando a mesma coluna de particionamento que a tabela subjacente.

> [!NOTE]
> Não é possível especificar um esquema de particionamento em um índice XML. Se a tabela base for particionada, o índice XML usará o mesmo esquema de partição que a tabela.

Para obter mais informações sobre particionamento de índices, consulte [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

ON _filegroup_name_      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior)

Cria o índice especificado no grupo de arquivos especificado. Se nenhum local for especificado e a tabela ou exibição não for particionada, o índice usará o mesmo grupo de arquivos que a tabela ou exibição subjacente. O grupo de arquivos já deve existir.

ON **"** default **"**      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Cria o índice especificado no mesmo esquema de partição ou grupo de arquivos que a tabela ou a exibição.

Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e precisa ser delimitado, como em ON **"** default **"** ou ON **[** default **]** . Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

> [!NOTE]
> "default" não indica o grupo de arquivos padrão de banco de dados no contexto de CREATE INDEX. Isso é diferente de CREATE TABLE, em que "default" localiza a tabela no grupo de arquivos de banco de dados padrão.

[ FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL" } ]      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior)

Especifica a colocação de dados FILESTREAM para a tabela quando um índice clusterizado é criado. A cláusula FILESTREAM_ON permite mover os dados FILESTREAM para outro grupo de arquivos ou esquema de partição FILESTREAM.

_filestream_filegroup_name_ é o nome de um grupo de arquivos FILESTREAM. O grupo de arquivos deve ter um arquivo definido para o grupo de arquivos usando uma instrução [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) ou [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md); caso contrário, será gerado um erro.

Se a tabela for particionada, a cláusula FILESTREAM_ON deverá ser incluída e especificar um esquema de partição de grupo de arquivos FILESTREAM que use a mesma função de partição e colunas de partição que o esquema de partição da tabela. Caso contrário, será gerado um erro.

Se a tabela não estiver particionada, a coluna FILESTREAM não poderá ser particionada. Os dados FILESTREAM da tabela devem ser armazenados em um único grupo de arquivos que é especificado na cláusula FILESTREAM_ON.

`FILESTREAM_ON NULL` poderá ser especificado em uma instrução CREATE INDEX se um índice clusterizado estiver sendo criado e a tabela não contiver uma coluna FILESTREAM.

Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).

**\<object>::=**      

É o objeto totalmente qualificado ou não totalmente qualificado a ser indexado.

_database_name_      
É o nome do banco de dados.

*schema_name*      
É o nome do esquema ao qual a tabela ou exibição pertence.

*table_or_view_name*      
É o nome da tabela ou exibição que será indexada.

A exibição deve ser definida com SCHEMABINDING para criar um índice nela. Um índice clusterizado exclusivo deve ser criado em uma exibição antes que qualquer índice não clusterizado seja criado. Para obter mais informações sobre exibições indexadas, consulte a seção Comentários.

A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o objeto pode ser uma tabela armazenada com um índice columnstore clusterizado.

O [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] dá suporte ao formato de nome de três partes _database_name_.[_schema_name_]._object_name_ quando *database_name* é o banco de dados atual ou o _database_name_ é `tempdb` e o _object_name_ começa com #.

**\<relational_index_option\>::=**       
Especifica as opções a serem usadas ao criar o índice.

PAD_INDEX = { ON | **OFF** }      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica o preenchimento do índice. O padrão é OFF.

ATIVADO      
O percentual de espaço livre especificado por *fillfactor* é aplicado às páginas de nível intermediário do índice.

OFF ou _fillfactor_ não está especificado      
As páginas de nível intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, considerando o conjunto de chaves em páginas intermediárias.

A opção PAD_INDEX só é útil quando FILLFACTOR é especificado, porque PAD_INDEX usa a porcentagem especificada por FILLFACTOR. Se a porcentagem especificada para FILLFACTOR não for grande o suficiente para permitir uma linha, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] substituirá a porcentagem internamente para permitir o valor mínimo. O número de linhas em uma página de índice intermediária nunca é menor do que dois, independentemente de quão baixo seja o valor de _fillfactor_.

Na sintaxe compatível com versões anteriores, WITH PAD_INDEX é equivalente a WITH PAD_INDEX = ON.

FILLFACTOR **=** _fillfactor_      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou recriação do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. Se *fillfactor* for 100, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará índices com páginas de folha preenchidas até a capacidade total.

A configuração FILLFACTOR se aplica somente quando o índice é criado ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para exibir a configuração do fator de preenchimento, use a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

> [!IMPORTANT]
> A criação de um índice clusterizado com FILLFACTOR inferior a 100 afeta a quantidade de espaço de armazenamento ocupado pelos dados, porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.

Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).

SORT_IN_TEMPDB = { ON | **OFF** }      

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica se os resultados de classificação temporários devem ser armazenados no **tempdb**. O padrão é OFF, exceto para a hiperescala do Banco de Dados SQL do Azure. Para todas as operações de build de índice em hiperescala, SORT_IN_TEMPDB está sempre ativo, independentemente da opção especificada, a menos que se use um rebuild de índice retomável.

ATIVADO      
Os resultados de classificação intermediários usados para criar o índice são armazenados no **tempdb**. Isso poderá reduzir o tempo necessário para criar um índice se **tempdb** estiver em um conjunto de discos diferente do banco de dados de usuário. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.

OFF      
Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.

Além do espaço necessário no banco de dados de usuário para criar o índice, **tempdb** deve ter aproximadamente a mesma quantidade de espaço adicional para conter os resultados de classificação intermediários. Para obter mais informações, consulte a [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).

Na sintaxe compatível com versões anteriores, WITH SORT_IN_TEMPDB é equivalente a WITH SORT_IN_TEMPDB = ON.

IGNORE_DUP_KEY = { ON | **OFF** }      
Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. A opção não tem nenhum efeito ao executar [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) ou [UPDATE](../../t-sql/queries/update-transact-sql.md). O padrão é OFF.

ATIVADO      
Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.

OFF      
Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.

IGNORE_DUP_KEY não pode ser definido como ON para índices criados em uma exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.

Para exibir IGNORE_DUP_KEY, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

Na sintaxe compatível com versões anteriores, WITH IGNORE_DUP_KEY é equivalente a WITH IGNORE_DUP_KEY = ON.

STATISTICS_NORECOMPUTE = { ON | **OFF**}      
Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.

ATIVADO      
As estatísticas desatualizadas não são recalculadas automaticamente.

OFF      
A atualização automática de estatísticas está habilitada.

Para restaurar a atualização automática de estatísticas, defina STATISTICS_NORECOMPUTE como OFF ou execute UPDATE STATISTICS sem a cláusula NORECOMPUTE.

> [!IMPORTANT]
> Se o recálculo automático de estatísticas de distribuição for desabilitado, o otimizador de consulta possivelmente ficará impedido de selecionar planos de execução ideais para consultas que envolvam a tabela.

Na sintaxe compatível com versões anteriores, WITH STATISTICS_NORECOMPUTE é equivalente a WITH STATISTICS_NORECOMPUTE = ON.

STATISTICS_INCREMENTAL = { ON | **OFF** }     

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Quando estiver **ON**, as estatísticas serão criadas conforme as estatísticas de partição. Quando estiver **OFF**, a árvore de estatísticas será removida e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] calculará as estatísticas novamente. O padrão é **OFF**.

Se as estatísticas por partição não tiverem suporte, a opção será ignorada e um aviso será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:

- Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.
- Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.
- Estatísticas criadas em bancos de dados somente leitura.
- Estatísticas criadas em índices filtrados.
- Estatísticas criadas em exibições.
- Estatísticas criadas em tabelas internas.
- Estatísticas criadas com índices espaciais ou índices XML.

DROP_EXISTING = { ON | **OFF** }      
É uma opção para remover e recompilar o índice clusterizado ou não clusterizado existente com as especificações da coluna modificada e manter o mesmo nome para o índice. O padrão é OFF.

ATIVADO      
Especifica remover e recompilar o índice existente, que deve ter o mesmo nome que o parâmetro *index_name*.

OFF      
Especifica não remover e recompilar o índice existente. O SQL Server exibirá um erro se o nome do índice especificado já existir.

Com DROP_EXISTING, é possível alterar:

- Um índice rowstore não clusterizado para um índice rowstore clusterizado.

Com DROP_EXISTING, não é possível alterar:

- Um índice rowstore clusterizado para um índice rowstore não clusterizado.
- Um índice columnstore clusterizado para qualquer tipo de índice de rowstore.

Na sintaxe compatível com versões anteriores, WITH DROP_EXISTING é equivalente a WITH DROP_EXISTING = ON.

ONLINE = { ON | **OFF** }      
Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF.

> [!IMPORTANT]
> As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).

ATIVADO      
Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Ele permite o prosseguimento de consultas ou atualizações feitas na tabela e nos índices subjacentes. No início da operação, um bloqueio Compartilhado (S) é mantido no objeto de origem por um período muito curto. Ao término da operação, por um curto período de tempo, um bloqueio S (Compartilhado) será adquirido na origem se um índice não clusterizado estiver sendo criado; ou um bloqueio de modificação de esquema (SCH-M) será adquirido quando um índice clusterizado for criado ou descartado online e quando um índice clusterizado ou não clusterizado estiver sendo recriado. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local.

OFF      
Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Uma operação de índice offline que cria, recria ou cancela um índice clusterizado ou recria ou cancela um índice não clusterizado, adquire um bloqueio de esquema de modificação (Sch-M) na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT.

Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  

Índices, inclusive aqueles em tabelas temporárias globais, podem ser criados online exceto nos seguintes casos:

- Índice XML
- Índice em uma tabela temporária local
- Índice clusterizado exclusivo inicial em uma exibição
- Índices clusterizados desabilitados
- Índices columnstore
- Índice clusterizado se a tabela subjacente contiver tipos de dados LOB (**image**, **ntext**, **text**) e tipos de dados espaciais
- As colunas **varchar(max)** e **varbinary(max)** não podem fazer parte de um índice. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], quando uma tabela contém as colunas **varchar(max)** ou **varbinary(max)** , um índice clusterizado contendo outras colunas pode ser criado ou recriado usando a opção **ONLINE**. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não permite a opção **ONLINE** quando a tabela base contém as colunas **varchar(max)** ou **varbinary(max)**

Para obter mais informações, consulte [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md).

RESUMABLE **=** { ON | **OFF**}      

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

 Especifica se uma operação de índice online é retomável.

 ATIVADO      
A operação do índice é retomável.

 OFF      
A operação do índice não é retomável.

MAX_DURATION **=** *time* [**MINUTES**] usado com **RESUMABLE = ON** (exige **ONLINE = ON**)   

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Indica o tempo (um valor inteiro especificado em minutos) pelo qual um uma operação de índice online retomável é executada antes de ser colocada em pausa.

> [!IMPORTANT]
> Para obter mais informações sobre operações de índice que podem ser executadas online, consulte [Diretrizes para operações de índice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

> [!NOTE] 
> Não há suporte para recompilações de índice online retomáveis em índices columnstore.

ALLOW_ROW_LOCKS = { **ON** | OFF }      
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica se bloqueios de linha são permitidos. O padrão é ON.

ATIVADO      
Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.

OFF      
Bloqueios de linha não são usados.

ALLOW_PAGE_LOCKS = { **ON** | OFF }      
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica se bloqueios de página são permitidos. O padrão é ON.

ATIVADO      
Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.

OFF      
Bloqueios de página não são usados.

OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** }      
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica se a contenção de inserção de última página será ou não otimizada. O padrão é OFF. Confira a seção sobre [Chaves sequenciais](#sequential-keys) para saber mais.

MAXDOP = *max_degree_of_parallelism*      
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Substitui a opção de configuração **max degree of parallelism** enquanto durar a operação do índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.

*max_degree_of_parallelism* pode ser:

1      
Suprime a geração de plano paralelo.

\>1      
Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado, ou menos, com base na carga de trabalho atual do sistema.

0 (padrão)      
Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.

 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).

> [!NOTE]
> As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos compatíveis com as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Edições e recursos compatíveis com SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) e [Edições e recursos compatíveis com SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).

DATA_COMPRESSION      
Especifica a opção de compactação de dados para o índice, número de partição ou intervalo de partições especificado. As opções são as descritas a seguir:

Nenhuma      
O índice ou as partições especificadas não são compactados.

ROW      
O índice ou as partições especificadas são compactados com o uso da compactação de linha.

PAGE      
O índice ou as partições especificadas são compactados com o uso da compactação de página.

Para obter mais informações sobre compactação, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [ **,** ..._n_ ] **)**       
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se o índice não for particionado, o argumento ON PARTITIONS irá gerar um erro. Se a cláusula ON PARTITIONS não for fornecida, a opção DATA_COMPRESSION será aplicada a todas as partições de um índice particionado.

\<partition_number_expression> pode ser especificado das seguintes maneiras:

- Forneça o número de uma partição, por exemplo: ON PARTITIONS (2).
- Forneça os números de várias partições individuais separados por vírgulas, por exemplo: ON PARTITIONS (1, 5).
- Forneça os intervalos e as partições individuais, por exemplo: ON PARTITIONS (2, 4, 6 TO 8).

\<range> pode ser especificado como números de partição separados pela palavra TO, por exemplo: `ON PARTITIONS (6 TO 8)`.

 Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção DATA_COMPRESSION mais de uma vez, por exemplo:

```sql
REBUILD WITH
(
  DATA_COMPRESSION = NONE ON PARTITIONS (1),
  DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
  DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
);
```

## <a name="remarks"></a>Comentários
A instrução CREATE INDEX é otimizada como qualquer outra consulta. Para salvar as operações de E/S, o processador de consultas pode optar por examinar outro índice em vez de executar um exame de tabela. A operação de classificação pode ser eliminada em algumas situações. Em computadores com multiprocessadores, CREATE INDEX pode usar mais processadores para executar operações de exame e classificação associadas à criação do índice, exatamente como fazem outras consultas. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).

A operação de criação de índice poderá ser registrada minimamente se o modelo de recuperação de banco de dados for definido como bulk-logged ou simples.

Os índices podem ser criados em uma tabela temporária. Quando a tabela for removida ou a sessão encerrada, os índices serão removidos.

Um índice clusterizado pode ser criado em uma variável de tabela quando uma chave primária é criada. Quando a consulta é concluída ou a sessão é encerrada, o índice é removido.

Os índices dão suporte a propriedades estendidas.

## <a name="clustered-indexes"></a>Índices clusterizados
Criar um índice clusterizado em uma tabela (heap) ou descartar e recriar um índice clusterizado existente requer workspace adicional disponível no banco de dados, para acomodar a classificação de dados e uma cópia temporária da tabela original ou dos dados do índice clusterizado existente. Para obter mais informações sobre índices clusterizados, confira [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md) e o [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

## <a name="nonclustered-indexes"></a>Índices não clusterizados
A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você pode criar um índice não clusterizado em uma tabela armazenada como um índice columnstore clusterizado. Se você primeiro criar um índice não clusterizado em uma tabela armazenada como um índice clusterizado ou heap, o índice persistirá se você depois converter a tabela em um índice columnstore clusterizado. Também não é necessário remover o índice não clusterizado ao recompilar o índice columnstore clusterizado.

Limitações e restrições:

- A opção `FILESTREAM_ON` não é válida quando você cria um índice não clusterizado em uma tabela armazenada como um índice columnstore clusterizado.

## <a name="unique-indexes"></a>Índices exclusivos
Quando existe um índice exclusivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se há valores duplicados sempre que dados são adicionados por operações de inserção. As operações de inserção que geram valores de chave duplicados são revertidas, e o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe uma mensagem de erro. Isso acontece mesmo que a operação de inserção altere muitas linhas, mas crie apenas uma duplicata. Se for feita uma tentativa de inserir dados para os quais há um índice exclusivo e a cláusula IGNORE_DUP_KEY for definida como ON, somente as linhas que violarem o índice UNIQUE falharão.

## <a name="partitioned-indexes"></a>Índices particionados
Índices particionados são criados e mantidos de uma maneira semelhante às tabelas particionadas, mas, como índices comuns, são tratados como objetos de banco de dados separados. É possível haver um índice particionado em uma tabela não particionada, bem como é possível ter um índice não particionado em uma tabela particionada.

Se você estiver criando um índice em uma tabela particionada e não especificar um grupo de arquivos para colocar o índice, ele será particionado da mesma maneira que a tabela subjacente. Isso ocorre porque, por padrão, os índices são colocados nos mesmos grupos de arquivos que suas tabelas subjacentes e, para uma tabela particionada, no mesmo esquema de partição que usa as mesmas colunas de particionamento. Quando o índice usa o mesmo esquema de partição e coluna de particionamento que a tabela, ele é *alinhado* à tabela.

> [!WARNING]
> É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações. É recomendável usar índices alinhados apenas quando o número de partições for maior que 1.000.

Ao particionar um índice clusterizado não exclusivo, por padrão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona quaisquer colunas de particionamento à lista de chaves de índice clusterizado, se já não estiverem especificadas.

As exibições indexadas podem ser criadas em tabelas particionadas da mesma maneira que os índices em tabelas. Para obter mais informações sobre índices particionados, confira [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md) e o [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Para obter as estatísticas dos índices particionados ao examinar todas as linhas da tabela, use `CREATE STATISTICS` ou `UPDATE STATISTICS` com a cláusula `FULLSCAN`.

## <a name="filtered-indexes"></a>Índices filtrados
Índice filtrado é um índice não clusterizado otimizado, adequado a consultas que selecionam uma pequena porcentagem de linhas de uma tabela. Ele usa um predicado de filtro para indexar uma parte dos dados na tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta, além de reduzir custos de armazenamento e de manutenção.

### <a name="required-set-options-for-filtered-indexes"></a>Opções SET necessárias para índices filtrados

As opções SET na coluna Valor necessário são necessárias sempre que ocorrer alguma das seguintes condições:

- Criar um índice filtrado.
- A operação INSERT, UPDATE, DELETE ou MERGE modificar os dados de um índice filtrado.
- O índice filtrado é usado pelo otimizador de consulta para produzir o plano de consulta.

    |Opções Set|Valor obrigatório|Valor do servidor padrão|Padrão<br /><br /> Valor OLE DB e ODBC|Padrão<br /><br /> Valor da DB-Library|
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|
    |ANSI_NULLS|ATIVADO|ATIVADO|ATIVADO|OFF|
    |ANSI_PADDING|ATIVADO|ATIVADO|ATIVADO|OFF|
    |ANSI_WARNINGS*|ATIVADO|ATIVADO|ATIVADO|OFF|
    |ARITHABORT|ATIVADO|ATIVADO|OFF|OFF|
    |CONCAT_NULL_YIELDS_NULL|ATIVADO|ATIVADO|ATIVADO|OFF|
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|
    |QUOTED_IDENTIFIER|ATIVADO|ATIVADO|ATIVADO|OFF|
  
     * A definição de ANSI_WARNINGS como ON definirá ARITHABORT implicitamente como ON quando o nível de compatibilidade do banco de dados estiver definido como 90 ou mais. Se o nível de compatibilidade do banco de dados estiver definido como 80 ou menos, a opção ARITHABORT deverá ser definida explicitamente como ON.

Se as opções SET estiverem incorretas, as seguintes condições poderão ocorrer:

- O índice filtrado não é criado.
- O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e reverte as instruções INSERT, UPDATE, DELETE ou MERGE que alteram os dados no índice.
- O otimizador de consulta não considera o índice no plano de execução para qualquer instrução Transact-SQL.

 Para obter mais informações sobre índices filtrados, confira [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md) e o [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

## <a name="spatial-indexes"></a>Índices espaciais
Para obter informações sobre índices espaciais, veja [CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md) e [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).

## <a name="xml-indexes"></a>Índices XML
Para informações sobre índices XML, veja [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md) e [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).

## <a name="index-key-size"></a>Tamanho de chave de índice
O tamanho máximo para uma chave de índice é de 900 bytes para um índice clusterizado e de 1.700 bytes para um índice não clusterizado. (Antes de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o limite foi sempre 900 bytes). Os índices nas colunas **varchar** que excederem o limite de bytes poderão ser criados se os dados existentes nas colunas não excederem o limite bytes no momento da criação do índice; entretanto, as ações subsequentes de inserção ou atualização nas colunas que fazem com que o tamanho total seja maior que o limite de bytes falharão. A chave de um índice clusterizado não pode conter colunas **varchar** que tenham dados existentes na unidade de alocação ROW_OVERFLOW_DATA. Se um índice clusterizado for criado em uma coluna **varchar** e os dados existentes estiverem na unidade de alocação IN_ROW_DATA, as ações subsequentes de inserção ou atualização na coluna que faria o push dos dados da linha apresentarão falha.

Índices não clusterizados podem incluir colunas não chave no nível folha do índice. Essas colunas não são consideradas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao calcular o tamanho da chave de índice. Para obter mais informações, confira [Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md) e o [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

> [!NOTE]
> Quando as tabelas são particionadas, se as colunas de chave de particionamento ainda não estiverem presentes em um índice clusterizado não exclusivo, elas poderão ser adicionadas ao índice pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O tamanho combinado das colunas indexadas (sem contar as colunas incluídas) mais qualquer coluna de particionamento adicionada não pode exceder 1.800 bytes em um índice clusterizado não exclusivo.

## <a name="computed-columns"></a>Colunas computadas
Os índices podem ser criados em colunas computadas. Além disso, as colunas computadas podem ter a propriedade PERSISTED. Isso significa que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena os valores computados na tabela e os atualiza quando as outras colunas das quais a coluna computada depende são atualizadas. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa esses valores persistentes ao criar um índice na coluna e quando o índice é referenciado em uma consulta.

Uma coluna computada deve ser determinística e precisa para ser indexada. Entretanto, o uso da propriedade PERSISTED expande o tipo das colunas computadas indexáveis para incluir:

- Colunas computadas baseadas nas funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e CLR, e métodos de tipo CLR definidos pelo usuário que são marcados como determinísticos pelo usuário.
- Colunas computadas baseadas em expressões que são determinísticas, conforme definidas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], mas imprecisas.

As colunas computadas persistentes requerem que as seguintes opções SET sejam definidas como mostrado na seção anterior [Opções SET necessárias para índices filtrados](#required-set-options-for-filtered-indexes).

A restrição UNIQUE ou PRIMARY KEY pode conter uma coluna computada contanto que satisfaça todas as condições para indexação. Especificamente, a coluna computada deve ser determinística e precisa ou determinística e persistente. Para obter mais informações sobre determinismo de funções, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).

Colunas computadas derivadas dos tipos de dados **image**, **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e **xml** podem ser indexadas como coluna chave ou não chave incluída, desde que o tipo de dados da coluna computada seja permitido como uma coluna chave ou não chave de índice. Por exemplo, não é possível criar um índice XML primário em uma coluna **xml** computada. Se o tamanho da chave de índice exceder 900 bytes, uma mensagem de aviso será exibida.

Criar um índice em uma coluna computada pode causar a falha de uma operação de inserção ou atualização que tenha funcionado anteriormente. Essa falha pode ocorrer quando a coluna computada resultar em erro aritmético. Por exemplo, na tabela a seguir, embora a coluna computada `c` resulte em um erro aritmético, a instrução INSERT funciona.

```sql
CREATE TABLE t1 (a INT, b INT, c AS a/b);
INSERT INTO t1 VALUES (1, 0);
```

Se, em vez disso, depois de criar a tabela, você criar um índice em uma coluna computada `c`, a mesma instrução `INSERT` agora falhará.

```sql
CREATE TABLE t1 (a INT, b INT, c AS a/b);
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);
INSERT INTO t1 VALUES (1, 0);
```

Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).

## <a name="included-columns-in-indexes"></a>Colunas incluídas em índices
As colunas não chave, chamadas de colunas incluídas, podem ser adicionadas ao nível folha de um índice não clusterizado para melhorar o desempenho da consulta ao abrangê-la. Isso quer dizer que todas as colunas referenciadas na consulta são incluídas no índice como colunas de chave ou não chave. Isso permite que o otimizador de consulta localize todas as informações necessárias de um exame de índice; os dados de tabela ou de índice clusterizado não são acessados. Para obter mais informações, confira [Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md) e o [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

## <a name="specifying-index-options"></a>Especificando opções de índice
O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu novas opções de índice e também modifica o modo como as opções são especificadas. Na sintaxe compatível com versões anteriores, WITH *option_name* é equivalente a WITH **(** \<option_name> **= ON )** . Ao definir as opções de índice, aplicam-se as seguintes regras:

- Novas opções de índice só podem ser especificadas usando WITH (**_option\_name_ = ON | OFF**).
- As opções não podem ser especificadas com o uso de sintaxe compatível com versões anteriores e nova sintaxe na mesma instrução. Por exemplo, especificar WITH (**DROP_EXISTING, ONLINE = ON**) faz a instrução falhar.
- Ao criar um índice XML, as opções devem ser especificadas usando WITH (**_option_name_= ON | OFF**).

## <a name="drop_existing-clause"></a>Cláusula DROP_EXISTING
É possível usar a cláusula DROP_EXISTING para recriar o índice, adicionar ou descartar colunas, modificar opções, modificar a ordem de classificação de colunas, ou alterar o esquema de partição ou o grupo de arquivos.

Se o índice impuser uma restrição PRIMARY KEY ou UNIQUE e a definição de índice não for alterada de alguma maneira, o índice será descartado e recriado preservando a restrição existente. Entretanto, se a definição de índice for alterada, a instrução falhará. Para alterar a definição de uma restrição PRIMARY KEY ou UNIQUE, descarte a restrição e adicione uma restrição com a nova definição.

DROP_EXISTING melhora o desempenho quando você recria um índice clusterizado, com o mesmo conjunto de chaves ou um conjunto diferente, em uma tabela que também tenha índices não clusterizados. DROP_EXISTING substitui a execução de uma instrução DROP_INDEX no índice clusterizado antigo, seguida da execução de uma instrução CREATE_INDEX para o novo índice clusterizado. Os índices não clusterizados são recriados uma vez e, depois disso, somente se a definição de índice for alterada. A cláusula DROP_EXISTING não recria os índices não clusterizados quando a definição de índice tem o mesmo nome de índice, chave e colunas de partição, atributo de exclusividade e ordem de classificação que o índice original.

Os índices não clusterizados podem ser recriados ou não, mas sempre permanecem em seus grupos de arquivos ou esquemas de partição originais e usam as funções de partição originais. Se um índice clusterizado for recriado para um grupo de arquivos ou esquema de partição diferente, os índices não clusterizados não serão movidos para coincidir com o novo local do índice clusterizado. Portanto, mesmo os índices não clusterizados previamente alinhados ao índice clusterizado, podem não estar mais alinhados a ele. Para obter mais informações sobre o alinhamento de índices particionados, consulte [Índices e tabelas particionadas](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

A cláusula DROP_EXISTING não classificará os dados novamente se as mesmas colunas de chave de índice forem usadas na mesma ordem e com a mesma ordem crescente ou decrescente, a menos que a instrução de índice especifique um índice não clusterizado e a opção ONLINE seja definida como OFF. Se o índice clusterizado for desabilitado, a operação CREATE INDEX WITH DROP_EXISTING deverá ser executada com ONLINE definido como OFF. Se um índice não clusterizado for desabilitado e não for associado a um índice clusterizado desabilitado, a operação CREATE INDEX WITH DROP_EXISTING poderá ser executada com ONLINE definido como OFF ou ON.

> [!NOTE]
> Quando índices com 128 extensões ou mais são descartados ou recriados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.

## <a name="online-option"></a>Opção ONLINE
As diretrizes a seguir são aplicáveis ao executar operações de índice online:

- A tabela subjacente não pode ser alterada, truncada ou descartada quando uma operação de índice online estiver em andamento.
- É necessário espaço em disco temporário adicional durante a operação de índice.
- As operações online podem ser executadas em índices particionados e índices que contenham colunas computadas ou colunas incluídas persistentes.

Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).

### <a name="resumable-index-operations"></a><a name="resumable-indexes"></a>Operações de índice retomáveis
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

As diretrizes a seguir se aplicam a operações de índice retomável:

- A criação de índice online é especificada como retomável usando a opção `RESUMABLE = ON`.
- A opção RESUMABLE não persiste nos metadados para um determinado índice e se aplica somente à duração de uma instrução DDL atual. Portanto, a cláusula `RESUMABLE = ON` deve ser especificada explicitamente para habilitar a capacidade de retomada.
- Só há suporte para a opção MAX_DURATION na opção `RESUMABLE = ON`.
- A opção MAX_DURATION para RESUMABLE especifica o intervalo para um índice que está sendo recompilado. Depois que esse tempo é consumido, a recompilação de índice é colocada em pausa ou conclui sua execução. O usuário decide quando uma recompilação de um índice em pausa pode ser retomada. O **tempo** em minutos para MAX_DURATION deve ser maior que 0 minutos e menor ou igual uma semana (7 \* 24 \* 60 = 10080 minutos). Ter uma longa pausa para uma operação de índice pode afetar o desempenho de DML em uma tabela específica, bem como a capacidade de disco de banco de dados, já que tanto o original quanto o recém-criado exigem espaço em disco e precisam ser atualizados durante as operações DML. Se a opção MAX_DURATION for omitida, a operação de índice continuará até sua conclusão ou até que ocorra uma falha.
- Para pausar imediatamente a operação de índice, você pode interromper (Ctrl-C) o comando em andamento, executar o comando [ALTER INDEX](alter-index-transact-sql.md) PAUSE ou executar o comando `KILL <session_id>`. Depois que o comando for colocado em pausa, ele poderá ser retomado usando o comando [ALTER INDEX](alter-index-transact-sql.md).
- Executar novamente a instrução CREATE INDEX original para o índice retomável retoma automaticamente uma operação de criação de índice em pausa.
- Não há suporte para a opção `SORT_IN_TEMPDB = ON` no índice retomável.
- O comando DDL com `RESUMABLE = ON` não pode ser executado em uma transação explícita (não pode fazer parte do bloco TRAN ... COMMIT).
- Para retomar/anular uma recompilação/criação de índice, use a sintaxe [ALTER INDEX](alter-index-transact-sql.md) T-SQL

> [!NOTE]
> O comando DDL é executado até ser concluído, pausar ou falhar. Caso o comando pause, será emitido um erro indicando que a operação foi colocada em pausa e que a criação de índice não foi concluída. Para obter mais informações sobre o status atual do índice, veja [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). Como antes, no caso de uma falha, um erro será emitido também.

Para indicar que a criação de um índice é executada como uma operação retomável e para verificar seu estado de execução atual, confira [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md).

#### <a name="resources"></a>Recursos
Os recursos a seguir são necessários para a operação de criação de índice online retomável:

- Espaço adicional necessário para manter o índice que está sendo criado, incluindo o tempo em que o índice está em pausa
- Taxa de transferência de log adicional durante a fase de classificação. O uso de espaço de log geral para índice retomável é menor em comparação com a criação de índice online regular e permite o truncamento de log durante a operação.
- Um estado DDL que impede qualquer modificação de DDL
- A limpeza de fantasma está bloqueada no índice no build pela duração da operação, em pausa e enquanto a operação está em execução.

#### <a name="current-functional-limitations"></a>Limitações funcionais atuais
A seguinte funcionalidade está desabilitada para operações de criação de índice retomáveis:

- Depois que uma operação de criação de índice online retomável é pausada, o valor inicial de MAXDOP não pode ser alterado
- Criar um índice que contém:

  - Coluna(s) calculada(s) ou TIMESTAMP como colunas de chave
  - Coluna LOB como coluna incluída para criação de índice retomável
  - Índice filtrado

## <a name="row-and-page-locks-options"></a>Opções de bloqueios de linha e de página
Quando a opção for `ALLOW_ROW_LOCKS = ON` e `ALLOW_PAGE_LOCK = ON`, os bloqueios em nível de linha, página e tabela serão permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.

Quando a opção for `ALLOW_ROW_LOCKS = OFF` e `ALLOW_PAGE_LOCK = OFF`, somente o bloqueio em nível de tabela será permitido ao acessar o índice.

## <a name="sequential-keys"></a>Chaves sequenciais
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

A contenção de inserção de última página é um problema de desempenho comum que ocorre quando um grande número de threads simultâneos tenta inserir linhas em um índice com uma chave sequencial. Um índice é considerado sequencial quando a coluna de chave à esquerda contém valores que sempre aumentam (ou diminuem), como uma coluna de identidade ou uma data que assume como padrão a data/hora atual. Como as chaves que estão sendo inseridas são sequenciais, todas as novas linhas serão inseridas no final da estrutura do índice – em outras palavras, na mesma página. Isso leva à contenção da página na memória que pode ser observada como vários threads aguardando PAGELATCH_EX para a página em questão.

Ativar a opção de índice OPTIMIZE_FOR_SEQUENTIAL_KEY permite uma otimização no mecanismo de banco de dados que ajuda a melhorar a taxa de transferência de inserções de alta simultaneidade em um índice. Ele se destina aos índices que têm uma chave sequencial e, portanto, estão sujeitos à contenção de inserção de última página, mas também pode ajudar com os índices que têm pontos de acesso em outras áreas da estrutura de índice de árvore B.

## <a name="viewing-index-information"></a>Exibindo informações de índice
Para retornar informações sobre índices, é possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema.

## <a name="data-compression"></a>Data Compression
Compactação de dados é descrita no tópico [Compactação de dados](../../relational-databases/data-compression/data-compression.md). A seguir estão os pontos-chave a serem considerados:

- A compactação pode permitir que mais linhas sejam armazenadas em uma página, mas não altera o tamanho máximo da linha.
- Páginas não folha de um índice não são compactadas por página, mas podem ser compactadas por linha.
- Cada índice não clusterizado tem uma configuração de compactação individual e não herda a configuração de compactação da tabela subjacente.
- Quando um índice clusterizado é criado em um heap, ele herda o estado de compactação do heap, a menos que um estado de compactação alternativo seja especificado.

As restrições a seguir se aplicam a índices particionados:

- Não será possível alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.
- O ALTER INDEX \<index>… REBUILD PARTITION ... recria a partição especificada do índice.
- O ALTER INDEX \<index>… REBUILD WITH... recria todas as partições do índice.

Para avaliar como a alteração do estado de compactação afetará uma tabela, um índice ou uma partição, use o procedimento armazenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .

## <a name="permissions"></a>Permissões
Requer a permissão `ALTER` na tabela ou exibição. O usuário deve ser membro da função de servidor fixa `sysadmin` ou das funções de banco de dados fixas `db_ddladmin` ou `db_owner`.

## <a name="limitations-and-restrictions"></a>Limitações e Restrições
No [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], não é possível criar:

- Um índice rowstore clusterizado ou não clusterizado em uma tabela de data warehouse quando já existe um índice columnstore. Esse comportamento é diferente do SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o que permite aos índices rowstore e columnstore coexistir na mesma tabela.
- Você não pode criar um índice em uma exibição.

## <a name="metadata"></a>Metadados
Para exibir informações sobre índices existentes, você pode consultar a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

## <a name="version-notes"></a>Notas de versão

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] não é compatível com as opções grupo de arquivos e fluxo de arquivos.

## <a name="examples-all-versions-uses-the-adventureworks-database"></a>Exemplos: Todas as versões. Usa o banco de dados AdventureWorks

### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>a. Criar um índice rowstore não clusterizado simples
Os exemplos a seguir criam um índice não clusterizado na coluna `VendorID` da tabela `Purchasing.ProductVendor`.

```sql
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);
```

### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. Criar um índice composto rowstore não clusterizado simples
O exemplo a seguir cria um índice composto não clusterizado nas colunas `SalesQuota` e `SalesYTD` da tabela `Sales.SalesPerson`.

```sql
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);
```

### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. Criar um índice em uma tabela em outro banco de dados
O exemplo a seguir cria um índice clusterizado na coluna `VendorID` da tabela `ProductVendor` no banco de dados `Purchasing`.

```sql
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);
```

### <a name="d-add-a-column-to-an-index"></a>D. Adicionar uma coluna a um índice
O exemplo a seguir cria o índice IX_FF com duas colunas da tabela dbo.FactFinance. A próxima instrução recompila o índice com mais uma coluna e mantém o nome existente.

```sql
CREATE INDEX IX_FF ON dbo.FactFinance (FinanceKey ASC, DateKey ASC);

-- Rebuild and add the OrganizationKey
CREATE INDEX IX_FF ON dbo.FactFinance (FinanceKey, DateKey, OrganizationKey DESC)
  WITH (DROP_EXISTING = ON);
```

## <a name="examples-sql-server-azure-sql-database"></a>Exemplos: SQL Server, Banco de Dados SQL do Azure

### <a name="e-create-a-unique-nonclustered-index"></a>E. Criando um índice não clusterizado exclusivo
O exemplo a seguir cria um índice não clusterizado exclusivo na coluna `Name` da tabela `Production.UnitMeasure` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O índice imporá a exclusividade dos dados inseridos na coluna `Name`.

```sql
CREATE UNIQUE INDEX AK_UnitMeasure_Name
  ON Production.UnitMeasure(Name);
```

A consulta a seguir testa a restrição de exclusividade tentando inserir uma linha com o mesmo valor que o de uma linha existente.

```sql
-- Verify the existing value.
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';
GO

INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)
  VALUES ('OC', 'Ounces', GETDATE());
```

A mensagem de erro resultante é:

```
Server: Msg 2601, Level 14, State 1, Line 1
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.
```

### <a name="f-use-the-ignore_dup_key-option"></a>F. Use a opção IGNORE_DUP_KEY
O exemplo a seguir demonstra o efeito da opção `IGNORE_DUP_KEY` inserindo várias linhas em uma tabela temporária primeiro com a opção definida como `ON` e, em seguida, com a opção definida como `OFF`. Uma única linha é inserida na tabela `#Test`, causando intencionalmente um valor duplicado quando a segunda instrução de várias linhas `INSERT` for executada. Uma contagem de linhas na tabela retorna o número de linhas inseridas.

```sql
CREATE TABLE #Test (C1 NVARCHAR(10), C2 NVARCHAR(50), C3 DATETIME);
GO

CREATE UNIQUE INDEX AK_Index ON #Test (C2)
  WITH (IGNORE_DUP_KEY = ON);
GO

INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;
GO

SELECT COUNT(*) AS [Number of rows] FROM #Test;
GO

DROP TABLE #Test;
GO
```

A seguir são apresentados os resultados da segunda instrução `INSERT`.

```cmd
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.

Number of rows
--------------
38
```

Observe que as linhas inseridas da tabela `Production.UnitMeasure` que não violaram a restrição de exclusividade foram inseridas com êxito. Um aviso foi emitido e a linha duplicada ignorada, mas a transação inteira não foi revertida.

As mesmas instruções são executadas novamente, mas com `IGNORE_DUP_KEY` definido como `OFF`.

```sql
CREATE TABLE #Test (C1 NVARCHAR(10), C2 NVARCHAR(50), C3 DATETIME);
GO

CREATE UNIQUE INDEX AK_Index ON #Test (C2)
  WITH (IGNORE_DUP_KEY = OFF);
GO

INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;
GO

SELECT COUNT(*) AS [Number of rows] FROM #Test;
GO

DROP TABLE #Test;
GO
```

A seguir são apresentados os resultados da segunda instrução `INSERT`.

```
Server: Msg 2601, Level 14, State 1, Line 5
Cannot insert duplicate key row in object '#Test' with unique index
'AK_Index'. The statement has been terminated.

Number of rows
--------------
1
```

Observe que nenhuma linha da tabela `Production.UnitMeasure` foi inserida na tabela, embora somente uma linha violasse a restrição de índice `UNIQUE`.

### <a name="g-using-drop_existing-to-drop-and-re-create-an-index"></a>G. Usando DROP_EXISTING para descartar e recriar um índice
O exemplo a seguir remove e recria um índice existente na coluna `ProductID` da tabela `Production.WorkOrder` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] usando a opção `DROP_EXISTING`. As opções `FILLFACTOR` e `PAD_INDEX` também são definidas.

```sql
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID
  ON Production.WorkOrder(ProductID)
    WITH (FILLFACTOR = 80,
      PAD_INDEX = ON,
      DROP_EXISTING = ON);
GO
```

### <a name="h-create-an-index-on-a-view"></a>H. Criar um índice em um modo de exibição
O exemplo a seguir cria uma exibição e um índice nessa exibição. Duas consultas que usam a exibição indexada são incluídas.

```sql
-- Set the options to support indexed views
SET NUMERIC_ROUNDABORT OFF;
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,
  QUOTED_IDENTIFIER, ANSI_NULLS ON;
GO

-- Create view with schemabinding
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL
  DROP VIEW Sales.vOrders;
GO

CREATE VIEW Sales.vOrders
  WITH SCHEMABINDING
AS
  SELECT SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Revenue,
    OrderDate, ProductID, COUNT_BIG(*) AS COUNT
  FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o
  WHERE od.SalesOrderID = o.SalesOrderID
  GROUP BY OrderDate, ProductID;
GO

-- Create an index on the view
CREATE UNIQUE CLUSTERED INDEX IDX_V1
  ON Sales.vOrders (OrderDate, ProductID);
GO

-- This query can use the indexed view even though the view is
-- not specified in the FROM clause.
SELECT SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Rev,
  OrderDate, ProductID
FROM Sales.SalesOrderDetail AS od
  JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID = o.SalesOrderID
    AND ProductID BETWEEN 700 AND 800
    AND OrderDate >= CONVERT(DATETIME, '05/01/2002', 101)
GROUP BY OrderDate, ProductID
ORDER BY Rev DESC;
GO

-- This query can use the above indexed view
SELECT OrderDate, SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Rev
FROM Sales.SalesOrderDetail AS od
  JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID = o.SalesOrderID
    AND DATEPART(mm, OrderDate) = 3
  AND DATEPART(yy, OrderDate) = 2002
GROUP BY OrderDate
ORDER BY OrderDate ASC;
GO
```

### <a name="i-create-an-index-with-included-non-key-columns"></a>I. Criando um índice com colunas incluídas (não chave)
O exemplo a seguir cria um índice não clusterizado com uma coluna de chave (`PostalCode`) e quatro colunas não chave (`AddressLine1`, `AddressLine2`, `City`, `StateProvinceID`). Uma consulta incluída pelo índice vem em seguida. Para exibir o índice que é selecionado pelo otimizador de consulta, no menu **Consulta** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione **Exibir Plano de Execução Real** antes de executar a consulta.

```sql
CREATE NONCLUSTERED INDEX IX_Address_PostalCode
  ON Person.Address (PostalCode)
  INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);
GO

SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode
FROM Person.Address
WHERE PostalCode BETWEEN N'98000' and N'99999';
GO
```

### <a name="j-create-a-partitioned-index"></a>J. Criar um índice particionado
O exemplo a seguir cria um índice particionado não clusterizado em `TransactionsPS1`, um esquema de partição existente no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Este exemplo pressupõe que o exemplo de índice particionado tenha sido instalado.

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID
  ON Production.TransactionHistory (ReferenceOrderID)
  ON TransactionsPS1 (TransactionDate);
GO
```

### <a name="k-creating-a-filtered-index"></a>K. Criando um índice filtrado
O exemplo a seguir cria um índice filtrado na tabela Production.BillOfMaterials do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O predicado de filtro pode incluir colunas que não sejam de chave no índice filtrado. O predicado deste exemplo seleciona apenas as linhas em que EndDate é não NULL.

```sql
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"
  ON Production.BillOfMaterials (ComponentID, StartDate)
  WHERE EndDate IS NOT NULL;
```

### <a name="l-create-a-compressed-index"></a>L. Criar um índice compactado
O exemplo a seguir cria um índice em uma tabela não particionada usando a compactação de linha.

```sql
CREATE NONCLUSTERED INDEX IX_INDEX_1
  ON T1 (C2)
  WITH (DATA_COMPRESSION = ROW);
GO
```

O exemplo a seguir cria um índice em uma tabela particionada usando a compactação de linha em todas as partições do índice.

```sql
CREATE CLUSTERED INDEX IX_PartTab2Col1
  ON PartitionTable1 (Col1)
  WITH (DATA_COMPRESSION = ROW);
GO
```

 O exemplo a seguir cria um índice em uma tabela particionada usando a compactação de página na partição `1` do índice e a compactação de linha nas partições `2` a `4` do índice.

```sql
CREATE CLUSTERED INDEX IX_PartTab2Col1
  ON PartitionTable1 (Col1)
  WITH (
    DATA_COMPRESSION = PAGE ON PARTITIONS(1),
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4)
  );
GO
```

### <a name="m-create-resume-pause-and-abort-resumable-index-operations"></a>M. Criar, retomar, pausar e anular operações de índice retomável
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
-- Execute a resumable online index create statement with MAXDOP=1
CREATE INDEX test_idx1 ON test_table (col1) WITH (ONLINE = ON, MAXDOP = 1, RESUMABLE = ON);

-- Executing the same command again (see above) after an index operation was paused, resumes automatically the index create operation.

-- Execute a resumable online index creates operation with MAX_DURATION set to 240 minutes. After the time expires, the resumable index create operation is paused.
CREATE INDEX test_idx2 ON test_table (col2) WITH (ONLINE = ON, RESUMABLE = ON, MAX_DURATION = 240);

-- Pause a running resumable online index creation
ALTER INDEX test_idx1 ON test_table PAUSE;
ALTER INDEX test_idx2 ON test_table PAUSE;

-- Resume a paused online index creation
ALTER INDEX test_idx1 ON test_table RESUME;
ALTER INDEX test_idx2 ON test_table RESUME;

-- Abort resumable index create operation which is running or paused
ALTER INDEX test_idx1 ON test_table ABORT;
ALTER INDEX test_idx2 ON test_table ABORT;
```

## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="n-basic-syntax"></a>N. Sintaxe básica
Criar, retomar, pausar e anular operações de índice retomável       

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
-- Execute a resumable online index create statement with MAXDOP=1
CREATE INDEX test_idx ON test_table WITH (ONLINE = ON, MAXDOP = 1, RESUMABLE = ON);

-- Executing the same command again (see above) after an index operation was paused, resumes automatically the index create operation.

-- Execute a resumable online index creates operation with MAX_DURATION set to 240 minutes. After the time expires, the resumable index create operation is paused.
CREATE INDEX test_idx ON test_table WITH (ONLINE = ON, RESUMABLE = ON, MAX_DURATION = 240);

-- Pause a running resumable online index creation
ALTER INDEX test_idx ON test_table PAUSE;

-- Resume a paused online index creation
ALTER INDEX test_idx ON test_table RESUME;

-- Abort resumable index create operation which is running or paused
ALTER INDEX test_idx ON test_table ABORT;
```

### <a name="o-create-a-nonclustered-index-on-a-table-in-the-current-database"></a>O. Criar um índice não clusterizado em uma tabela no banco de dados atual
O exemplo a seguir cria um índice não clusterizado na coluna `VendorID` da tabela `ProductVendor`.

```sql
CREATE INDEX IX_ProductVendor_VendorID
  ON ProductVendor (VendorID);
```

### <a name="p-create-a-clustered-index-on-a-table-in-another-database"></a>P. Criar um índice clusterizado em uma tabela em outro banco de dados
O exemplo a seguir cria um índice não clusterizado na coluna `VendorID` da tabela `ProductVendor` no banco de dados `Purchasing`.

```sql
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID
  ON Purchasing..ProductVendor (VendorID);
```
### <a name="q-create-an-ordered-clustered-index-on-a-table"></a>Q. Criar um índice clusterizado ordenado em uma tabela  
O exemplo a seguir cria um índice clusterizado ordenado nas colunas `c1` e `c2` da tabela `T1` no banco de dados `MyDB`.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX MyOrderedCCI ON MyDB.dbo.T1 
ORDER (c1, c2);

```

### <a name="r-convert-a-cci-to-an-ordered-clustered-index-on-a-table"></a>R. Converter um CCI em um índice clusterizado ordenado em uma tabela  
O exemplo a seguir converte o índice columnstore clusterizado existente em um índice columnstore clusterizado ordenado chamado `MyOrderedCCI` nas colunas `c1` e `c2` da tabela `T2` no banco de dados `MyDB`.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX MyOrderedCCI ON MyDB.dbo.T2
ORDER (c1, c2)
WITH (DROP_EXISTING = ON);

```

## <a name="see-also"></a>Consulte Também
[Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md)     
[Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)  
[Índices e ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md#indexes-and-alter-table)     
[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)     
[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)     
[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)     
[CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md)      
[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)     
[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)    
[CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md)     
[Tipos de dados](../../t-sql/data-types/data-types-transact-sql.md)    
[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)    
[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)    
[Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)     
[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)     
[sys.index_columns](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)    
[sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)     
[EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)     
