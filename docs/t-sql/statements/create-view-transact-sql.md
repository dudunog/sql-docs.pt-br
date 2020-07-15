---
title: CREATE VIEW (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de62120fd28e67c4323a88f73bc5bac939aedc64
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002495"
---
# <a name="create-view-transact-sql"></a>CREATE VIEW (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cria uma tabela virtual cujo conteúdo (colunas e linhas) é definido por uma consulta. Use esta instrução para criar uma exibição dos dados em uma ou mais tabelas no banco de dados. Por exemplo, uma exibição pode ser usada para as finalidades a seguir:  
  
-   Para focalizar, simplificar e personalizar a percepção que cada usuário tem do banco de dados.  
  
-   Como um mecanismo de segurança permitindo que os usuários acessem dados por meio da exibição, sem conceder permissões aos usuários para acessar diretamente as tabelas base subjacentes.  
  
-   Para fornecer uma interface compatível com versões anteriores para emular uma tabela cujo esquema foi alterado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] VIEW [ schema_name . ] view_name [ (column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ]   
[ ; ]  
  
<view_attribute> ::=   
{  
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE VIEW [ schema_name . ] view_name [  ( column_name [ ,...n ] ) ]   
AS <select_statement>   
[;]  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumentos
OR ALTER  
 **Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).   
  
 Altera condicionalmente a exibição somente se ela já existe. 
 
 *schema_name*  
 É o nome do esquema ao qual a exibição pertence.  
  
 *view_name*  
 É o nome da exibição. Os nomes de exibição devem seguir as regras para identificadores. A especificação do nome do proprietário da exibição é opcional.  
  
 *column*  
 É o nome a ser usado para uma coluna em uma exibição. O nome de coluna é necessário somente quando uma coluna é derivada de uma expressão aritmética, função ou constante, quando duas ou mais colunas puderem ter o mesmo nome, normalmente por causa de uma união, ou quando uma coluna em uma exibição tiver um nome especificado diferente daquele da coluna da qual ela é derivada. Nomes de coluna também podem ser atribuídos na instrução SELECT.  
  
 Se *column* não for especificado, as colunas de exibição adquirirão os mesmos nomes que as colunas na instrução SELECT.  
  
> [!NOTE]  
>  Nas colunas da exibição, as permissões de um nome de coluna são aplicadas por uma instrução CREATE VIEW ou ALTER VIEW, independentemente da fonte dos dados subjacentes. Por exemplo, se forem concedidas permissões na coluna **SalesOrderID** em uma instrução CREATE VIEW, uma instrução ALTER VIEW poderá nomear a coluna **SalesOrderID** com um nome de coluna diferente, como **OrderRef**, e ainda terá as permissões associadas à exibição usando **SalesOrderID**.  
  
 AS  
 Especifica as ações que a exibição deve executar.  
  
 *select_statement*  
 É a instrução SELECT que define a exibição. A instrução pode usar mais de uma tabela e outras exibições. Permissões apropriadas são necessárias para selecionar os objetos referenciados na cláusula SELECT da exibição criada.  
  
 Uma exibição não tem que ser um subconjunto simples das linhas e colunas de uma determinada tabela. Uma exibição pode ser criada usando mais de uma tabela ou outras exibições com uma cláusula VIEW de qualquer complexidade.  
  
 Em uma definição de exibição indexada, a instrução SELECT deve ser uma instrução de tabela simples ou uma JOIN de várias tabelas com agregação opcional.  
  
 As cláusulas SELECT em uma definição de exibição não podem incluir o seguinte:  
  
-   Uma cláusula ORDER BY, a não ser que exista também uma cláusula TOP na lista de seleção da instrução SELECT  
  
    > [!IMPORTANT]  
    >  A cláusula ORDER BY é usada apenas para determinar as linhas retornadas pela cláusula TOP ou OFFSET na definição da exibição. A cláusula ORDER BY não garante resultados ordenados quando a exibição é consultada, a menos que ORDER BY também seja especificada na consulta em si.  
  
-   A palavra-chave INTO  
  
-   A cláusula OPTION  
  
-   Uma referência para uma tabela temporária ou uma variável de tabela.  
  
 Como *select_statement* usa a instrução SELECT, é válido usar as dicas \<join_hint> e \<table_hint> conforme especificado na cláusula FROM. Para obter mais informações, veja [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) e [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md). 
  
 Funções e várias instruções SELECT separadas por UNION ou UNION ALL podem ser usadas em *select_statement*.  
  
 CHECK OPTION  
 Força que todas as instruções de modificação de dados sejam executadas em relação à exibição para seguir o conjunto de critérios dentro da *select_statement*. Quando uma linha é modificada através de uma exibição, WITH CHECK OPTION verifica se os dados permanecem visíveis na exibição depois que a modificação é confirmada.  
  
> [!NOTE]  
>  Qualquer atualização executada diretamente em tabelas subjacentes de uma exibição não são verificadas na exibição, mesmo que CHECK OPTION seja especificada.  
  
 ENCRYPTION  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Criptografa as entradas em [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) que contêm o texto da instrução CREATE VIEW. Usar WITH ENCRYPTION impede que a exibição seja publicada como parte da Replicação do SQL Server.  
  
 SCHEMABINDING  
 Associa a exibição ao esquema da tabela ou tabelas subjacentes. Quando SCHEMABINDING for especificado, a tabela ou tabelas base não poderão ser modificadas de um modo que possam afetar a definição da exibição. A própria definição da exibição, primeiro, deve ser modificada ou descartada para remover as dependências na tabela a ser modificada. Quando você usa SCHEMABINDING, o *select_statement* deve incluir os nomes de duas partes (_esquema_ **.** _objeto_) de tabelas, exibições ou funções definidas pelo usuário que são referenciadas. Todos os objetos referenciados devem estar no mesmo banco de dados.  
  
 As exibições ou tabelas que participam de uma exibição criada com a cláusula SCHEMABINDING não podem ser descartadas, a menos que a exibição seja descartada ou alterada de modo a não ter mais associação de esquema. Caso contrário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro. Além disso, haverá falha na execução de instruções ALTER TABLE nas tabelas que participam de exibições com associação de esquema quando essas instruções afetarem a definição da exibição.  
  
 VIEW_METADATA  
 Especifica que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará às APIs DB-Library, ODBC e OLE DB as informações de metadados sobre a exibição, em vez da tabela ou tabelas base, quando metadados do modo de procura forem solicitados para uma consulta que faz referência à exibição. Metadados do modo de procura são metadados adicionais que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna para essas APIs do lado do cliente. Esses metadados permitem que as APIs do lado do cliente implementem cursores atualizáveis do lado do cliente. Os metadados do modo de procura incluem informações sobre a tabela base às quais as colunas do conjunto de resultados pertencem.  
  
 Para exibições criadas com VIEW_METADATA, os metadados do modo de procura retornam o nome da exibição e não os nomes de tabela base quando descreverem colunas da exibição no conjunto de resultados.  
  
 Quando uma exibição é criada usando WITH VIEW_METADATA, todas as suas colunas, com exceção de uma coluna **timestamp**, serão atualizáveis se a exibição tiver gatilhos INSTEAD OF INSERT ou INSTEAD OF UPDATE. Para obter mais informações sobre exibições atualizáveis, consulte Comentários.  
  
## <a name="remarks"></a>Comentários  
 A exibição só pode ser criada no banco de dados atual. O CREATE VIEW deve ser a primeira instrução em um lote de consulta. Uma exibição pode ter, no máximo, 1.024 partições.  
  
 Ao fazer uma consulta através de uma exibição, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se todos os objetos de banco de dados referenciados em algum lugar da instrução existem, se são válidos no contexto da instrução e se as instruções de modificação de dados não violam nenhuma regra de integridade de dados. Uma verificação que falha retorna uma mensagem de erro. Uma verificação com êxito traduz a ação em uma ação na tabela ou tabelas subjacentes.  
  
 Se uma exibição depender de uma tabela ou exibição descartada, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] produzirá uma mensagem de erro quando alguém tentar usá-la. Se uma nova tabela ou exibição for criada e a estrutura da tabela não for alterada na tabela base anterior para substituir a descartada, a exibição se tornará utilizável novamente. Se a nova tabela ou estrutura de exibição for alterada, a exibição deverá ser descartada e recriada.  
  
 Se uma exibição não for criada com a cláusula SCHEMABINDING, execute [sp_refreshview](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md) quando forem feitas alterações aos objetos subjacentes à exibição que afetem a definição desta. Caso contrário, a exibição poderá gerar resultados inesperados quando consultada.  
  
 Quando uma exibição é criada, as informações sobre ela são armazenadas nas seguintes exibições do catálogo: [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md), [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) e [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md). O texto da instrução CREATE VIEW é armazenado na exibição do catálogo [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
 Uma consulta que usa um índice em uma exibição definida com expressões **numeric** ou **float** pode ter um resultado diferente de uma consulta semelhante que não usa o índice ou a exibição. Essa diferença pode ser causada por erros de arredondamento durante as ações INSERT, DELETE ou UPDATE em tabelas subjacentes.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] salva as configurações de QUOTED_IDENTIFIER Fixo e ANSI_NULLS quando uma exibição é criada. Essas configurações originais são usadas para analisar a exibição quando a ela é usada. Portanto, qualquer configuração de sessão de cliente para SET QUOTED_IDENTIFIER e SET ANSI_NULLS não afeta a definição da exibição quando a exibição é acessada.  
  
## <a name="updatable-views"></a>Exibições atualizáveis  
 É possível modificar os dados de uma tabela base subjacente através de uma exibição, contanto que as seguintes condições sejam verdadeiras:  
  
-   Todas as modificações, inclusive as instruções UPDATE, INSERT e DELETE, devem referenciar colunas de apenas uma tabela base.  
  
-   As colunas a serem modificadas na exibição devem referenciar diretamente os dados subjacentes das colunas da tabela. As colunas não podem ser derivadas de qualquer outro modo, como pelo seguinte:  
  
    -   Uma função de agregação: AVG, COUNT, SUM, MIN, MAX, GROUPING, STDEV, STDEVP, VAR e VARP.  
  
    -   Uma computação. A coluna não pode ser computada de uma expressão que utiliza outras colunas. As colunas formadas com o uso dos operadores de conjunto UNION, UNION ALL, CROSSJOIN, EXCEPT e INTERSECT resultam em uma computação e também não são atualizáveis.  
  
-   As colunas modificadas não são afetadas pelas cláusulas GROUP BY, HAVING ou DISTINCT.  
  
-   TOP não é usado em nenhum lugar na *select_statement* da exibição junto com a cláusula WITH CHECK OPTION.  
  
 As restrições anteriores aplicam-se a todas as subconsultas da cláusula FROM da exibição, exatamente como se aplicam à própria exibição. Em geral, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser capaz de rastrear sem ambiguidade as modificações da definição da exibição em uma tabela base. Para obter mais informações, confira [Modificar dados por meio de uma exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
 Se as restrições anteriores impediram a modificação de dados direta através de uma exibição, considere as seguintes opções:  
  
-   **Gatilhos INSTEAD OF**  
  
     Os gatilhos INSTEAD OF podem ser criados em uma exibição para torná-la atualizável. O gatilho INSTEAD OF é executado em vez da instrução de modificação de dados na qual ele é definido. Esse gatilho deixa o usuário especificar o conjunto de ações que devem acontecer para processar a instrução de modificação de dados. Portanto, se um gatilho INSTEAD OF existir para uma exibição em uma instrução de modificação de dados específica (INSERT, UPDATE ou DELETE), a exibição correspondente será atualizável através dessa instrução. Para obter mais informações sobre gatilhos INSTEAD OF, veja [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md).  
  
-   **Exibições particionadas**  
  
     Se a exibição for uma exibição particionada, ela será atualizável, sujeita a determinadas restrições. Quando necessário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] distingue as exibições particionadas locais como as exibições nas quais todas as tabelas participantes e a exibição estão na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e as exibições particionadas distribuídas como as exibições nas quais pelo menos uma das tabelas na exibição reside em um servidor diferente ou servidor remoto.  
  
## <a name="partitioned-views"></a>Exibições particionadas  
 Uma exibição particionada é uma exibição definida por uma UNION ALL das tabelas de membro estruturadas da mesma maneira, mas armazenadas separadamente como tabelas múltiplas na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um grupo de instâncias autônomas de servidores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], chamados de servidores de banco de dados federados.  
  
> [!NOTE]  
>  O método preferencial para o particionamento dos locais de dados para um servidor é através de tabelas particionadas. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Ao criar um esquema de particionamento, devem estar claro quais dados pertencem a cada partição. Por exemplo, os dados para a tabela `Customers` são distribuídos em três tabelas membro, em três locais de servidor: `Customers_33` no `Server1`, `Customers_66` no `Server2` e `Customers_99` no `Server3`.  
  
 Uma exibição particionada no `Server1` é definida da seguinte maneira:  
  
```sql
--Partitioned view as defined on Server1  
CREATE VIEW Customers  
AS  
--Select from local member table.  
SELECT *  
FROM CompanyData.dbo.Customers_33  
UNION ALL  
--Select from member table on Server2.  
SELECT *  
FROM Server2.CompanyData.dbo.Customers_66  
UNION ALL  
--Select from member table on Server3.  
SELECT *  
FROM Server3.CompanyData.dbo.Customers_99;  
```  
  
 Em geral, uma exibição é considerada particionada se for da seguinte forma:  
  
```syntaxsql
SELECT <select_list1>  
FROM T1  
UNION ALL  
SELECT <select_list2>  
FROM T2  
UNION ALL  
...  
SELECT <select_listn>  
FROM Tn;  
```  
  
## <a name="conditions-for-creating-partitioned-views"></a>Condições para criar exibições particionadas  
  
1.  A `list` de seleção  
  
    -   Na lista de colunas da definição de exibição, selecione todas as colunas nas tabelas membro.  
  
    -   Assegure que as colunas na mesma posição ordinal de cada `select list` sejam do mesmo tipo, incluindo ordenações. Não é suficiente para as colunas serem tipos conversíveis implicitamente, como em geral é o caso de UNION.  
  
         Além disso, pelo menos uma coluna (por exemplo, `<col>`) deve aparecer em todas as listas de seleção na mesma posição ordinal. Esse `<col>` deve ser definido de uma forma que as tabelas membro `T1, ..., Tn` tenham restrições CHECK `C1, ..., Cn` definidas em `<col>`, respectivamente.  
  
         A restrição `C1` definida na tabela `T1` deve ser da seguinte forma:  
  
        ```syntaxsql
        C1 ::= < simple_interval > [ OR < simple_interval > OR ...]  
        < simple_interval > :: =   
        < col > { < | > | \<= | >= | = < value >}   
        | < col > BETWEEN < value1 > AND < value2 >  
        | < col > IN ( value_list )  
        | < col > { > | >= } < value1 > AND  
        < col > { < | <= } < value2 >  
        ```
  
    -   As restrições devem ser de uma forma que qualquer valor especificado de `<col>` possa satisfazer, no máximo, uma das restrições `C1, ..., Cn` para que as restrições não formem um conjunto de intervalos desunidos ou não sobrepostos. A coluna `<col>` na qual as restrições desunidas são definidas é chamada de coluna de particionamento. Observe que a coluna de particionamento pode ter nomes diferentes nas tabelas subjacentes. As restrições devem estar em um estado habilitado e confiável para que atendam às condições de coluna de particionamento mencionadas anteriormente. Se as restrições forem desabilitadas, reabilite a verificação de restrição usando a opção CHECK CONSTRAINT *constraint_name* de ALTER TABLE e a opção WITH CHECK para validá-las.  
  
         Os exemplos a seguir mostram conjuntos válidos de restrições:  
  
        ```syntaxsql
        { [col < 10], [col between 11 and 20] , [col > 20] }  
        { [col between 11 and 20], [col between 21 and 30], [col between 31 and 100] }  
        ```  
  
    -   A mesma coluna não pode ser usada várias vezes na lista de seleção.  
  
2.  Coluna de particionamento  
  
    -   A coluna de particionamento faz parte da PRIMARY KEY da tabela.  
  
    -   Ela não pode ser uma coluna computada, de identidade, padrão nem **timestamp**.  
  
    -   Se houver mais de uma restrição na mesma coluna em uma tabela membro, o Mecanismo de Banco de Dados irá ignorar todas as restrições e não irá considerá-las ao determinar se a exibição é particionada. Para conhecer as condições da exibição particionada, deve haver somente uma restrição de particionamento na coluna de particionamento.  
  
    -   Não há nenhuma restrição na capacidade de atualização da coluna de particionamento.  
  
3.  Tabelas membro ou tabelas subjacentes `T1, ..., Tn`  
  
    -   As tabelas podem ser tabelas locais ou tabelas de outros computadores que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] referenciadas através de um nome de quatro partes ou um nome baseado em OPENDATASOURCE ou OPENROWSET. A sintaxe OPENDATASOURCE e OPENROWSET pode especificar um nome de tabela, mas não uma consulta de passagem. Para obter mais informações, veja [OPENDATASOURCE &#40;Transact-SQL&#41; ](../../t-sql/functions/opendatasource-transact-sql.md) e [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
         Se uma ou mais das tabelas membro forem remotas, a exibição será chamada de exibição particionada distribuída, e as condições adicionais serão aplicadas. Elas são descritas posteriormente nesta seção.  
  
    -   A mesma tabela não pode aparecer duas vezes no conjunto de tabelas que estão sendo combinadas com a instrução UNION ALL.  
  
    -   As tabelas membro não podem ter índices criados em qualquer coluna computada na tabela.  
  
    -   As tabelas membro têm todas as restrições PRIMARY KEY no mesmo número de colunas.  
  
    -   Todas as tabelas de membro na exibição têm a mesma configuração de preenchimento ANSI. Isso pode ser definido usando a opção **user options** em **sp_configure** ou a instrução SET.  
  
## <a name="conditions-for-modifying-data-in-partitioned-views"></a>Condições para modificar dados em exibições particionadas  
 As seguintes restrições se aplicam a instruções que modificam dados nas exibições particionadas:  
  
-   A instrução INSERT fornece valores para todas as colunas na exibição, mesmo que as tabelas membro subjacentes tenham uma restrição DEFAULT para essas colunas ou que permitam valores nulos. Para essas colunas de tabela membro com definições DEFAULT, as instruções não podem usar a palavra-chave DEFAULT explicitamente.  
  
-   O valor a ser inserido na coluna de particionamento deverá satisfazer pelo menos uma das restrições subjacentes; caso contrário, a ação de inserção falhará com uma violação de restrição.  
  
-   As instruções UPDATE não podem especificar a palavra-chave DEFAULT como valor na cláusula SET, mesmo que a coluna tenha um valor DEFAULT definido na tabela membro correspondente.  
  
-   As colunas na exibição que estiverem em uma coluna de identidade de uma ou mais tabelas membro não poderão ser modificadas através de uma instrução INSERT ou UPDATE.  
  
-   Se uma das tabelas membro tiver uma coluna **timestamp**, os dados não poderão ser modificados por meio de uma instrução INSERT ou UPDATE.  
  
-   Se uma das tabelas membro tiver um gatilho ou uma restrição ON UPDATE CASCADE/SET NULL/SET DEFAULT ou ON DELETE CASCADE/SET NULL/SET DEFAULT, a exibição não poderá ser modificada.  
  
-   As ações INSERT, UPDATE e DELETE em uma exibição particionada não são permitidas quando há uma autojunção com a mesma exibição ou com qualquer uma das tabelas membro na instrução.  
  
-   Não há compatibilidade com a importação de dados em uma exibição particionada por **bcp** ou pelas instruções BULK INSERT e INSERT... SELECT * FROM OPENROWSET(BULK...). Entretanto, é possível inserir várias linhas em uma exibição particionada usando uma instrução [INSERT](../../t-sql/statements/insert-transact-sql.md).  
  
    > [!NOTE]  
    >  Para atualizar uma exibição particionada, o usuário deve ter as permissões INSERT, UPDATE e DELETE nas tabelas membro.  
  
## <a name="additional-conditions-for-distributed-partitioned-views"></a>Condições adicionais para exibições particionadas distribuídas  
 Para as exibições particionadas distribuídas (quando uma ou mais tabelas membro são remotas), são aplicáveis as seguintes condições adicionais:  
  
-   Uma transação distribuída será iniciada para garantir a atomicidade em todos os nós afetados pela atualização.  
  
-   Defina a opção XACT_ABORT SET para ON para que as instruções INSERT, UPDATE ou DELETE funcionem.  
  
-   Qualquer coluna nas tabelas remotas do tipo **smallmoney** referenciadas em uma exibição particionada são mapeadas como **money**. Portanto, as colunas correspondentes (na mesma posição ordinal na lista de seleção) nas tabelas locais também devem ser do tipo **money**.  
  
-   No nível de compatibilidade de banco de dados 110 e superiores, as colunas em tabelas remotas do tipo **smalldatatime** referenciadas em uma exibição particionada são mapeadas como **smalldatetime**. As colunas correspondentes (na mesma posição ordinal na lista de seleção) nas tabelas locais devem ser **smalldatetime**. Essa é uma alteração no comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nas quais qualquer coluna em tabelas remotas do tipo **smalldatetime** referenciadas em uma exibição particionada são mapeadas como **datetime** e as colunas correspondentes em tabelas locais devem ser do tipo **datetime**. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
-   Qualquer servidor vinculado na exibição particionada não pode ser um servidor vinculado de loopback. Este é um servidor vinculado que aponta para a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A configuração da opção SET ROWCOUNT é ignorada para ações INSERT, UPDATE e DELETE que envolvam exibições particionadas atualizáveis e tabelas remotas.  
  
 Quando as tabelas membro e a definição de exibição particionada estão em vigor, o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria planos inteligentes que usam consultas de forma eficiente para acessar dados de tabelas membro. Com as definições da restrição CHECK, o processador de consulta mapeia a distribuição de valores de chave nas tabelas membro. Quando um usuário emite uma consulta, o processador de consulta compara o mapa com os valores especificados na cláusula WHERE e cria um plano de execução com uma quantidade mínima de transferência de dados entre os servidores membro. Assim, embora algumas tabelas membro possam ser localizadas em servidores remotos, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resolve consultas distribuídas de forma que a quantidade de dados distribuídos a ser transferida seja mínima.  
  
## <a name="considerations-for-replication"></a>Considerações sobre replicação  
 Para criar exibições particionadas em tabelas membro envolvidas em replicação, as seguintes considerações são aplicáveis:  
  
-   Se as tabelas subjacentes estiverem envolvidas em replicação de mesclagem ou replicação transacional com assinaturas de atualização, verifique se a coluna **uniqueidentifier** também está incluída na lista de seleção. 
  
     Toda ação INSERT na exibição particionada deve fornecer um valor NEWID() para a coluna **uniqueidentifier**. As ações UPDATE na coluna **uniqueidentifier** devem fornecer NEWID() como o valor, pois a palavra-chave DEFAULT não pode ser usada.  
  
-   A replicação de atualizações feita usando a exibição é a mesma de quando as tabelas são replicadas em dois bancos de dados diferentes: as tabelas são atendidas por agentes de replicação diferentes e a ordem das atualizações não é garantida.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE VIEW no banco de dados e a permissão ALTER no esquema no qual a exibição está sendo criada.  
  
## <a name="examples"></a>Exemplos  

Os exemplos a seguir usam o banco de dados AdventureWorks 2012 ou AdventureWorksDW.  

### <a name="a-using-a-simple-create-view"></a>a. Usando uma CREATE VIEW simples  
 O exemplo a seguir cria uma exibição usando uma instrução `SELECT` simples. Uma exibição simples é útil quando uma combinação de colunas é consultada com frequência. Os dados dessa exibição vêm das tabelas `HumanResources.Employee` e `Person.Person` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Os dados fornecem o nome e informações de data de contratação dos funcionários da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. A exibição pode ser criada para a pessoa que cuida do controle de aniversários de trabalho, mas sem dar a essa pessoa acesso a todos os dados nessas tabelas.  
  
```sql
CREATE VIEW hiredate_view  
AS   
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate  
FROM HumanResources.Employee e   
JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
### <a name="b-using-with-encryption"></a>B. Usando WITH ENCRYPTION  
 O exemplo a seguir usa a opção `WITH ENCRYPTION` e mostra colunas computadas, colunas renomeadas e várias colunas.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql
CREATE VIEW Purchasing.PurchaseOrderReject  
WITH ENCRYPTION  
AS  
SELECT PurchaseOrderID, ReceivedQty, RejectedQty,   
    RejectedQty / ReceivedQty AS RejectRatio, DueDate  
FROM Purchasing.PurchaseOrderDetail  
WHERE RejectedQty / ReceivedQty > 0  
AND DueDate > CONVERT(DATETIME,'20010630',101) ;  
GO  
  
```  
  
### <a name="c-using-with-check-option"></a>C. Usando WITH CHECK OPTION  
 O exemplo a seguir mostra uma exibição chamada `SeattleOnly` que referencia cinco tabelas e permite que as modificações de dados se apliquem somente a funcionários que vivem em Seattle.  
  
```sql
CREATE VIEW dbo.SeattleOnly  
AS  
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode  
FROM HumanResources.Employee e  
INNER JOIN Person.Person p  
ON p.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN Person.BusinessEntityAddress bea   
    ON bea.BusinessEntityID = e.BusinessEntityID   
    INNER JOIN Person.Address a   
    ON a.AddressID = bea.AddressID  
    INNER JOIN Person.StateProvince sp   
    ON sp.StateProvinceID = a.StateProvinceID  
WHERE a.City = 'Seattle'  
WITH CHECK OPTION ;  
GO  
```  
  
### <a name="d-using-built-in-functions-within-a-view"></a>D. Usando funções internas em uma exibição  
 O exemplo a seguir mostra uma definição de exibição que inclui uma função interna. Ao usar funções, é necessário especificar um nome de coluna para a coluna derivada.  
  
```sql
CREATE VIEW Sales.SalesPersonPerform  
AS  
SELECT TOP (100) SalesPersonID, SUM(TotalDue) AS TotalSales  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > CONVERT(DATETIME,'20001231',101)  
GROUP BY SalesPersonID;  
GO  

```  
  
### <a name="e-using-partitioned-data"></a>E. Usando dados particionados  
 O exemplo a seguir usa as tabelas chamadas `SUPPLY1`, `SUPPLY2`, `SUPPLY3` e `SUPPLY4`. Essas tabelas correspondem às tabelas de fornecedor de quatro escritórios, localizados em países/regiões diferentes.  
  
```sql
--Create the tables and insert the values.  
CREATE TABLE dbo.SUPPLY1 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 1 and 150),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY2 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 151 and 300),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY3 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 301 and 450),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY4 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 451 and 600),  
supplier CHAR(50)  
);  
GO  
--Create the view that combines all supplier tables.  
CREATE VIEW dbo.all_supplier_view  
WITH SCHEMABINDING  
AS  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY1  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY2  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY3  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY4;  
GO
INSERT dbo.all_supplier_view VALUES ('1', 'CaliforniaCorp'), ('5', 'BraziliaLtd')    
, ('231', 'FarEast'), ('280', 'NZ')  
, ('321', 'EuroGroup'), ('442', 'UKArchip')  
, ('475', 'India'), ('521', 'Afrique');  
GO  
```  
  
## <a name="examples-sssdw-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-creating-a-simple-view"></a>F. Criando uma exibição simples  
 O exemplo a seguir cria uma exibição selecionando apenas algumas das colunas da tabela de origem.  
  
```sql
CREATE VIEW DimEmployeeBirthDates AS  
SELECT FirstName, LastName, BirthDate   
FROM DimEmployee;  
```  
  
### <a name="g-create-a-view-by-joining-two-tables"></a>G. Criar um modo de exibição unindo duas tabelas  
 O exemplo a seguir cria uma exibição usando uma instrução `SELECT` com um `OUTER JOIN`. Os resultados da consulta de junção preenchem a exibição.  
  
```sql
CREATE VIEW view1  
AS 
SELECT fis.CustomerKey, fis.ProductKey, fis.OrderDateKey, 
  fis.SalesTerritoryKey, dst.SalesTerritoryRegion  
FROM FactInternetSales AS fis   
LEFT OUTER JOIN DimSalesTerritory AS dst   
ON (fis.SalesTerritoryKey=dst.SalesTerritoryKey);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_refreshview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

