---
description: DROP INDEX (Transact-SQL)
title: DROP INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_INDEX_TSQL
- DROP INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- nonclustered indexes [SQL Server], removing
- MAXDOP index option, DROP INDEX statement
- index removal [SQL Server]
- spatial indexes [SQL Server], dropping
- removing indexes
- deleting indexes
- dropping indexes
- MOVE TO clause
- clustered indexes, removing
- indexes [SQL Server], dropping
- filtered indexes [SQL Server], dropping
- ONLINE option
- indexes [SQL Server], moving
- XML indexes [SQL Server], dropping
- DROP INDEX statement
ms.assetid: 2b1464c8-934c-405f-8ef7-2949346b5372
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 56b60757878fb14b48c4c89218296000113d7f1d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465967"
---
# <a name="drop-index-transact-sql"></a>DROP INDEX (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove um ou mais índices relacionais, espaciais, filtrados ou XML do banco de dados atual. É possível descartar um índice clusterizado e mover a tabela resultante para outro grupo de arquivos ou esquema de partição em uma única transação especificando a opção MOVE TO.  
  
 A instrução DROP INDEX não se aplica a índices criados definindo as restrições PRIMARY KEY ou UNIQUE. Para remover a restrição e o índice correspondente, use [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) com a cláusula DROP CONSTRAINT.  
  
> [!IMPORTANT]
>  A sintaxe definida em `<drop_backward_compatible_index>` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar essa sintaxe em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que usam atualmente o recurso. Em vez disso, use a sintaxe especificada em `<drop_relational_or_xml_index>`. Índices XML não podem ser descartados usando sintaxe compatível com versões anteriores.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server (All options except filegroup and filestream apply to Azure SQL Database.)  
  
DROP INDEX [ IF EXISTS ]   
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
| <drop_backward_compatible_index> [ ,...n ]  
}  
  
<drop_relational_or_xml_or_spatial_index> ::=  
    index_name ON <object>   
    [ WITH ( <drop_clustered_index_option> [ ,...n ] ) ]  
  
<drop_backward_compatible_index> ::=  
    [ owner_name. ] table_or_view_name.index_name  
  
<object> ::=  
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }  
  
<drop_clustered_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
  | ONLINE = { ON | OFF }  
  | MOVE TO { partition_scheme_name ( column_name )   
            | filegroup_name  
            | "default"   
            }  
  [ FILESTREAM_ON { partition_scheme_name   
            | filestream_filegroup_name   
            | "default" } ]  
}  
```  
  
```syntaxsql
-- Syntax for Azure SQL Database  
  
DROP INDEX  
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
}  
  
<drop_relational_or_xml_or_spatial_index> ::=   
    index_name ON <object>  
  
<object> ::=   
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
DROP INDEX index_name ON { database_name.schema_name.table_name | schema_name.table_name | table_name }  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente o índice somente se ele já existe.  
  
 *index_name*  
 É o nome do índice a ser descartado.  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or_view_name*  
 É o nome da tabela ou exibição associada ao índice. Índices espaciais têm suporte apenas em tabelas.  
  
 Para exibir um relatório dos índices em um objeto, use a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 O Banco de Dados SQL do Azure oferece suporte ao formato de nome de três partes database_name.[schema_name].object_name quando o database_name é o banco de dados atual ou o database_name é tempdb e o object_name começa com #.  
  
 \<drop_clustered_index_option>  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Controla opções de índice clusterizado. Essas opções não podem ser usadas com outros tipos de índice.  
  
 MAXDOP = *max_degree_of_parallelism*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (somente Níveis de Desempenho P2 e P3).  
  
 Substitui a opção de configuração **max degree of parallelism** enquanto durar a operação do índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
> [!IMPORTANT]  
>  MAXDOP não é permitido para índices espaciais nem XML.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ONLINE = ON | **OFF**  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF.  
  
 ATIVADO  
 Bloqueios de tabela não são mantidos a longo prazo. Isso permite que consultas ou atualizações na tabela subjacente continuem.  
  
 OFF  
 Os bloqueios de tabela são aplicados e a tabela fica indisponível durante a operação de índice.  
  
 A opção ONLINE pode ser especificada ao descartar índices clusterizados Para obter mais informações, consulte a seção Comentários.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MOVE TO { _partition\_scheme\_name_ **(** _column\_name_ **)**  | _filegroup\_name_ |  **"** default **"**  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] dá suporte a "padrão" como o nome do grupo de arquivos.  
  
 Especifica o local para onde mover as linhas de dados que atualmente estão no nível folha do índice clusterizado. Os dados são movidos para o novo local no formulário de um heap. É possível especificar um esquema de partição ou um grupo de arquivos como o novo local, mas o esquema de partição ou o grupo de arquivos deve existir. MOVE TO não é válido para exibições indexadas ou índices não clusterizados. Se um esquema de partição ou grupo de arquivos não estiver especificado, a tabela resultante estará localizada no mesmo esquema de partição ou grupo de arquivos definido para o índice clusterizado.  
  
 Se um índice clusterizado for descartado usando MOVE TO, todos os índice clusterizados na tabela base serão recriados, mas permanecerão em seus grupos de arquivos ou esquemas de partição originais. Se a tabela base for movida para um grupo de arquivos ou esquema de partição diferente, os índices não clusterizados não serão movidos para coincidir com o novo local da tabela base (heap). Portanto, mesmo que os índices não clusterizados tenham sido previamente alinhados com o índice clusterizado, eles não poderão mais ser alinhados com o heap. Para obter mais informações sobre o alinhamento de índices particionados, consulte [Índices e tabelas particionadas](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 _partition_scheme_name_ **(** _column_name_ **)**  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica um esquema de partição como o local para a tabela resultante. O esquema de partição já deve ter sido criado com a execução de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) ou [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). Se nenhum local estiver especificado e a tabela estiver particionada, a tabela será incluída no mesmo esquema de partição que o índice clusterizado existente.  
  
 O nome da coluna no esquema não é restringido às colunas na definição do índice. Qualquer coluna da tabela base pode ser especificada.  
  
 *filegroup_name*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Especifica um grupo de arquivos como o local para a tabela resultante. Se nenhum local estiver especificado e a tabela não estiver particionada, a tabela resultante será incluída no mesmo grupo de arquivos que o índice clusterizado. O grupo de arquivos já deve existir.  
  
 **"** default **"**  
 Especifica o local padrão para a tabela resultante.  
  
> [!NOTE]
>  Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e deve ser delimitado, como em MOVE TO **"** default **"** ou MOVE TO **[** default **]** . Se **"** default **"** for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FILESTREAM_ON { *partition_scheme_name* | *filestream_filegroup_name* |  **"** default **"** }  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Especifica o local para onde mover a tabela FILESTREAM que atualmente está no nível folha do índice clusterizado. Os dados são movidos para o novo local no formulário de um heap. É possível especificar um esquema de partição ou um grupo de arquivos como o novo local, mas o esquema de partição ou o grupo de arquivos deve existir. FILESTREAM ON não é válido para exibições indexadas nem índices não clusterizados. Se um esquema de partição não estiver especificado, os dados estarão localizados no mesmo esquema de partição definido para o índice clusterizado.  
  
 *partition_scheme_name*  
 Especifica um esquema de partição para os dados FILESTREAM. O esquema de partição já deve ter sido criado com a execução de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) ou [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). Se nenhum local estiver especificado e a tabela estiver particionada, a tabela será incluída no mesmo esquema de partição que o índice clusterizado existente.  
  
 Se você especificar um esquema de partição para MOVE TO, deverá usar o mesmo esquema de partição para FILESTREAM ON.  
  
 *filestream_filegroup_name*  
 Especifica um grupo de arquivos FILESTREAM para dados FILESTREAM. Se nenhum local estiver especificado e a tabela não estiver particionada, os dados serão incluídos no grupo de arquivos FILESTREAM padrão.  
  
 **"** default **"**  
 Especifica o local padrão para os dados FILESTREAM.  
  
> [!NOTE]
>  Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e deve ser delimitado, como em MOVE TO **"** default **"** ou MOVE TO **[** default **]** . Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Quando um índice não clusterizado é descartado, a definição do índice é removida dos metadados e as páginas de dados do índice (a árvore B) são removidas dos arquivos do banco de dados. Quando um índice clusterizado é descartado, a definição do índice é removida dos metadados e as linhas de dados armazenadas no nível folha do índice clusterizado são armazenadas na tabela não ordenada resultante, um heap. Todo o espaço ocupado anteriormente pelo índice é recuperado. Em seguida, esse espaço pode ser usado para qualquer objeto de banco de dados.  
  
 Um índice não poderá ser descartado se o grupo de arquivos no qual está localizado estiver offline ou definido como somente leitura.  
  
 Quando o índice clusterizado de uma exibição indexada é descartado, todos os índices não clusterizados e estatísticas criadas automaticamente na mesma exibição são descartados automaticamente. As estatísticas criadas manualmente não são descartadas.  
  
 A sintaxe _table\_or\_view\_name_ **.** _index\_name_ é mantida para que haja compatibilidade com versões anteriores. Um índice XML ou espacial não pode ser descartado usando a sintaxe compatível com versões anteriores.  
  
 Quando índices com 128 extensões ou mais são descartados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.  
  
 Algumas vezes, os índices são descartados e recriados para reorganizar ou reconstruir o índice, como para aplicar um novo fator de preenchimento ou para reorganizar dados após um carregamento em massa. Para fazer isso, é mais eficiente usar [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), principalmente para índices clusterizados. ALTER INDEX REBUILD tem otimizações para evitar a sobrecarga da reconstrução de índices não clusterizados.  
  
## <a name="using-options-with-drop-index"></a>Usando opções com DROP INDEX  
 Você pode definir as seguintes opções de índice ao remover um índice clusterizado: MAXDOP, ONLINE e MOVE TO.  
  
 Use MOVE TO para descartar o índice clusterizado e mover a tabela resultante para outro grupo de arquivos ou esquema de partição em uma única transação.  
  
 Quando ONLINE = ON é especificado, as consultas e modificações nos dados subjacentes e os índices não clusterizados associados não são bloqueados pela transação DROP INDEX. Apenas um índice clusterizado pode ser descartado online de cada vez. Para obter uma descrição completa da opção ONLINE, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 Não é possível remover um índice clusterizado online se o índice está desabilitado em uma exibição ou conter colunas **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** ou **xml** nas linhas de dados no nível folha.  
  
 O uso das opções ONLINE = ON e MOVE TO requer espaço em disco temporário adicional.  
  
 Após a remoção de um índice, o heap resultante é mostrado na exibição do catálogo **sys.indexes** com NULL na coluna **name**. Para exibir o nome da tabela, una **sys.indexes** com **sys.tables** em **object_id**. Para ver uma consulta de exemplo, consulte o exemplo D.  
  
 Em computadores com multiprocessadores que estão executando o [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] ou posterior, DROP INDEX pode usar mais processadores para executar operações de exame e de classificação associadas ao descarte do índice clusterizado, exatamente como fazem outras consultas. É possível configurar manualmente o número de processadores usados para executar a instrução DROP INDEX especificando a opção de índice MAXDOP. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 Quando um índice clusterizado é descartado, as partições de heap correspondentes mantêm sua configuração de compactação de dados, a menos que o esquema de particionamento seja modificado. Se o esquema de particionamento for alterado, todas as partições serão reconstruídas para um estado não compactado (DATA_COMPRESSION = NONE). As duas etapas a seguir são necessárias para descartar um índice clusterizado e alterar o esquema de particionamento:  
  
1.  Descarte o índice clusterizado.  
  
2.  Modifique a tabela usando uma opção ALTER TABLE... REBUILD... especificando a opção de compactação.  
  
Quando um índice clusterizado é descartado OFFLINE, apenas os níveis superiores dos índices clusterizados são removidos, portanto, a operação é bastante rápida. Quando um índice clusterizado é removido ONLINE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recria o heap duas vezes, uma para a etapa 1 e outra para a etapa 2. Para obter mais informações sobre a compactação de dados, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
## <a name="xml-indexes"></a>Índices XML  
 Não é possível especificar opções ao remover um índice XML. Além disso, não é possível usar a sintaxe _table\_or\_view\_name_ **.** _index\_name_. Quando um índice XML primário é descartado, todos os índices XML secundários associados são descartados automaticamente. Para obter mais informações, veja [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="spatial-indexes"></a>Índices espaciais  
 Índices espaciais têm suporte apenas em tabelas. Ao remover um índice espacial, não é possível especificar nenhuma opção nem usar **.** _index\_name_. A sintaxe correta é a seguinte:  
  
 DROP INDEX *spatial_index_name* ON *spatial_table_name*;  
  
 Para obter mais informações sobre índices espaciais, consulte [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP INDEX, no mínimo a permissão ALTER na tabela ou exibição é necessária. Essa permissão é concedida por padrão à função de servidor fixa **sysadmin** e às funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-an-index"></a>a. Descartando um índice  
 O exemplo a seguir exclui o índice `IX_ProductVendor_VendorID` na tabela `ProductVendor` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
DROP INDEX IX_ProductVendor_BusinessEntityID   
    ON Purchasing.ProductVendor;  
GO  
```  
  
### <a name="b-dropping-multiple-indexes"></a>B. Descartando vários índices  
 O exemplo a seguir exclui dois índices em uma única transação no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
DROP INDEX  
    IX_PurchaseOrderHeader_EmployeeID ON Purchasing.PurchaseOrderHeader,  
    IX_Address_StateProvinceID ON Person.Address;  
GO  
```  
  
### <a name="c-dropping-a-clustered-index-online-and-setting-the-maxdop-option"></a>C. Descartando um índice clusterizado online e definindo a opção MAXDOP  
 O exemplo a seguir exclui um índice clusterizado com a opção `ONLINE` definida como `ON` e `MAXDOP` definida como `8`. Como a opção MOVE TO não foi especificada, a tabela resultante é armazenada no mesmo grupo de arquivos que o índice. Este exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
```sql  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials WITH (ONLINE = ON, MAXDOP = 2);  
GO  
```  
  
### <a name="d-dropping-a-clustered-index-online-and-moving-the-table-to-a-new-filegroup"></a>D. Descartando um índice clusterizado online e movendo a tabela para um novo grupo de arquivos  
 O exemplo a seguir exclui um índice clusterizado online e move a tabela resultante (heap) para o grupo de arquivos `NewGroup` usando a cláusula `MOVE TO` . As exibições do catálogo `sys.indexes`, `sys.tables`e `sys.filegroups` são consultadas para verificar o posicionamento do índice e da tabela nos grupos de arquivos antes e depois da movimentação. (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], é possível usar a sintaxe DROP INDEX IF EXISTS.)  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
```sql  
--Create a clustered index on the PRIMARY filegroup if the index does not exist.  
CREATE UNIQUE CLUSTERED INDEX  
    AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
        ON Production.BillOfMaterials (ProductAssemblyID, ComponentID,   
        StartDate)  
    ON 'PRIMARY';  
GO  
-- Verify filegroup location of the clustered index.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U')  
GO  
--Create filegroup NewGroup if it does not exist.  
IF NOT EXISTS (SELECT name FROM sys.filegroups  
                WHERE name = N'NewGroup')  
    BEGIN  
    ALTER DATABASE AdventureWorks2012  
        ADD FILEGROUP NewGroup;  
    ALTER DATABASE AdventureWorks2012  
        ADD FILE (NAME = File1,  
            FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\File1.ndf')  
        TO FILEGROUP NewGroup;  
    END  
GO  
--Verify new filegroup  
SELECT * from sys.filegroups;  
GO  
-- Drop the clustered index and move the BillOfMaterials table to  
-- the Newgroup filegroup.  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials   
    WITH (ONLINE = ON, MOVE TO NewGroup);  
GO  
-- Verify filegroup location of the moved table.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U');  
GO  
```  
  
### <a name="e-dropping-a-primary-key-constraint-online"></a>E. Descartando uma restrição PRIMARY KEY online  
 Índices criados em decorrência da criação de restrições PRIMARY KEY ou UNIQUE não podem ser descartados usando DROP INDEX. Eles são descartados usando a instrução ALTER TABLE DROP CONSTRAINT. Para obter mais informações, consulte [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 O exemplo a seguir exclui um índice clusterizado com uma restrição PRIMARY KEY descartando a restrição. A tabela `ProductCostHistory` não tem nenhuma restrição FOREIGN KEY. Se tivesse, essas restrições precisariam ser removidas primeiro.  
  
```sql  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
```  
  
### <a name="f-dropping-an-xml-index"></a>F. Descartando um índice XML  
 O exemplo a seguir remove um índice XML na tabela `ProductModel` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
DROP INDEX PXML_ProductModel_CatalogDescription   
    ON Production.ProductModel;  
```  
  
### <a name="g-dropping-a-clustered-index-on-a-filestream-table"></a>G. Descartando um índice clusterizado em uma tabela FILESTREAM  
 O exemplo a seguir exclui um índice clusterizado online e move a tabela resultante (heap) e os dados FILESTREAM para o esquema de partição `MyPartitionScheme` usando as cláusulas `MOVE TO` e `FILESTREAM ON`.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
```sql  
DROP INDEX PK_MyClusteredIndex   
    ON dbo.MyTable   
    WITH (MOVE TO MyPartitionScheme,  
          FILESTREAM_ON MyPartitionScheme);  
GO  
```  

  
## <a name="see-also"></a>Consulte Também  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  


