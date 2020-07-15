---
title: EXECUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74ab018b017b675e08abb53036f88c3eaf2e5618
ms.sourcegitcommit: 05fdc50006a9abdda79c3a4685b075796068c4fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84748595"
---
# <a name="execute-transact-sql"></a>EXECUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Executa uma cadeia de caracteres de comando, uma cadeia de caracteres em um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um dos seguintes módulos: procedimento armazenado do sistema, procedimento armazenado definido pelo usuário, procedimento armazenado CLR, função de valor escalar definida pelo usuário ou procedimento armazenado estendido. A instrução EXECUTE pode ser usada para enviar comandos de passagem aos servidores vinculados. Além disso, o contexto no qual uma cadeia de caracteres ou comando é executado pode ser definido explicitamente. É possível definir metadados para o conjunto de resultados usando as opções do WITH RESULT SETS.
  
> [!IMPORTANT]  
>  Antes de chamar EXECUTE com uma cadeia de caracteres, valide a cadeia de caracteres. Nunca execute um comando construído por uma entrada de usuário que não foi validada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
O bloco de código a seguir mostra a sintaxe no SQL Server 2019. Como alternativa, em vez disso, confira a [sintaxe no SQL Server 2017 e versões anteriores](execute-transact-sql.md?view=sql-server-2017). 

```syntaxsql
-- Syntax for SQL Server 2019
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
    [ AT DATA_SOURCE data_source_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
::: moniker-end

::: monikerRange=">=sql-server-2016 ||=sqlallproducts-allversions"

O bloco de código a seguir mostra a sintaxe no SQL Server 2017 e versões anteriores. Como alternativa, em vez disso, confira a [sintaxe no SQL Server 2019](execute-transact-sql.md?view=sql-server-ver15).


```syntaxsql
-- Syntax for SQL Server 2017 and earleir  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
::: moniker-end

  
```syntaxsql
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```syntaxsql
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```

  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  


  
## <a name="arguments"></a>Argumentos  
 @*return_status*  
 É uma variável de inteiro opcional que armazena o status de retorno de um módulo. Essa variável deve ser declarada no lote, procedimento armazenado ou função para ser usada antes em uma instrução EXECUTE.  
  
 Quando usada para invocar uma função definida pelo usuário com valor escalar, a variável @*return_status* pode ser de qualquer tipo de dados escalar.  
  
 *module_name*  
 É o nome totalmente qualificado do procedimento armazenado ou do valor escalar da função a ser chamada, definida pelo usuário. Os nomes de módulos devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Os nomes de procedimentos armazenados estendidos sempre têm diferenciação entre maiúsculas e minúsculas, independentemente da ordenação do servidor.  
  
 Um módulo que tenha sido criado em outro banco de dados poderá ser executado se o usuário que estiver executando o módulo for o proprietário ou se tiver permissão apropriada para executá-lo no referido banco de dados. Um módulo poderá ser executado em outro servidor que executa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o usuário que estiver executando o módulo tiver a permissão apropriada para usar esse servidor (acesso remoto) e executar o módulo no referido banco de dados. Se você especificar um nome de servidor mas não especificar um nome de banco de dados, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] procurará o módulo no banco de dados padrão do usuário.  
  
 ;*number*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 É um inteiro opcional usado para agrupar procedimentos do mesmo nome. Esse parâmetro não é usado para procedimentos armazenados estendidos.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Para obter mais informações sobre grupos de procedimentos, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 @*module_name_var*  
 É o nome de uma variável localmente definida que representa um nome de módulo.  
  
 Isso pode ser uma variável que contém o nome de uma função escalar definida pelo usuário compilada nativamente.  
  
 @*parameter*  
 É o parâmetro do *module_name*, conforme definido no módulo. Os nomes de parâmetro devem ser precedidos pelo sinal de arroba (@). Quando usados com o formato @*parameter_name*=*value*, os nomes de parâmetro e constantes não precisam ser fornecidos na ordem em que são definidos no módulo. Porém, se o formato @*parameter_name*=*value* for usado para um parâmetro, ele deverá ser usado para todos os parâmetros seguintes.  
  
 Por padrão, os parâmetros são anuláveis.  
  
 *value*  
 É o valor do parâmetro a ser informado ao módulo ou comando de passagem. Se não forem especificados nomes de parâmetro, os valores de parâmetro deverão ser fornecidos na ordem definida no módulo.  
  
 Na execução dos comandos de passagem em servidores vinculados, a ordem dos valores de parâmetro dependerá do provedor OLE DB do servidor vinculado. A maioria dos provedores OLE DB associa valores para os parâmetros da esquerda para a direita.  
  
 Se o valor de um parâmetro for o nome de um objeto, cadeia de caracteres ou qualificado por um nome de esquema ou nome de banco de dados, o nome todo deverá ficar dentro de aspas simples. Se o valor de um parâmetro for uma palavra-chave, a palavra-chave deverá ficar dentro de aspas duplas.  
  
Se você passar uma única palavra que não começa com `@` e que não está entre aspas, por exemplo, se você esquecer `@` em um nome de parâmetro, a palavra será tratada como uma cadeia de caracteres nvarchar, apesar das aspas ausentes.

 Se um padrão estiver definido no módulo, um usuário poderá executar o módulo sem especificar um parâmetro.  
  
 O padrão também pode ser NULL. Geralmente, a definição de módulo especificará a ação a ser tomada se um valor de parâmetro for NULL.  
  
 @*variable*  
 É a variável que armazena um parâmetro ou um parâmetro de retorno.  
  
 OUTPUT  
 Especifica que o módulo ou a cadeia de caracteres de comando deve retornar um parâmetro. O parâmetro correspondente no módulo ou na cadeia de caracteres de comando também deve ter sido criado com o uso da palavra-chave OUTPUT. Use essa palavra-chave quando você usar variáveis de cursor como parâmetros.  
  
 Se *value* for definido como OUTPUT de um módulo executado em um servidor vinculado, as alterações feitas no @*parameter* correspondente pelo Provedor OLE DB serão copiadas novamente para a variável no final da execução do módulo.  
  
 Se os parâmetros OUTPUT estiverem sendo usados e a intenção for usar os valores retornados em outras instruções no lote ou módulo de chamada, o valor do parâmetro deverá ser passado como uma variável, como @*parameter* = @*variable*. Não é possível executar um módulo especificando OUTPUT para um parâmetro que não esteja definido como OUTPUT no módulo. Não é possível passar constantes ao módulo usando OUTPUT; o parâmetro de retorno requer um nome de variável. O tipo de dados da variável deve ser declarado e ter um valor atribuído antes da execução do procedimento.  
  
 Quando EXECUTE é usado em um procedimento armazenado remoto ou para executar um comando de passagem em um servidor vinculado, os parâmetros OUTPUT não podem ser nenhum dos tipos de dados LOB (objeto grande).  
  
 Os parâmetros de retorno podem ser de qualquer tipo de dados, exceto os tipos de dados LOB.  
  
 DEFAULT  
 Fornece o valor padrão do parâmetro como definido no módulo. Quando o módulo esperar um valor para um parâmetro que não tem um padrão definido e houver um parâmetro ausente ou a palavra-chave DEFAULT estiver especificada, ocorrerá um erro.  
  
 @*string_variable*  
 É o nome de uma variável local. @*string_variable* pode ser qualquer tipo de dados **char**, **varchar**, **nchar** ou **nvarchar**. Incluem os tipos de dados **(max)** .  
  
 [N] '*tsql_string*'  
 É uma cadeia de caracteres constante. *tsql_string* pode ser qualquer tipo de dados **nvarchar** ou **varchar**. Se N for incluído, a cadeia de caracteres será interpretada como o tipo de dados **nvarchar**.  
  
 AS \<context_specification>  
 Especifica o contexto no qual a instrução é executada.  
  
 LOGIN  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica que o contexto para ser representado é um logon. O escopo de personificação é o servidor.  
  
 USER  
 Especifica que o contexto a ser representado é um usuário no banco de dados atual. O escopo de representação é restrito ao banco de dados atual. Uma opção de contexto para um usuário de banco de dados não herda as permissões em nível de servidor desse usuário.  
  
> [!IMPORTANT]  
>  Enquanto a opção de contexto para o usuário do banco de dados estiver ativa, qualquer tentativa de acessar os recursos fora do banco de dados causará a falha da instrução. Isso inclui instruções USE *database*, consultas distribuídas e consultas que referenciam outro banco de dados usando identificadores de três ou quatro partes.  
  
 '*name*'  
 É um usuário ou nome de logon válido. *name* deve ser membro da função de servidor fixa sysadmin ou existir como uma entidade de segurança em [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) ou [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), respectivamente.  
  
 *name* não pode ser uma conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT AUTHORITY\LocalSystem.  
  
 Para obter mais informações, consulte [Especificando um nome de logon ou usuário](#_user) mais adiante neste tópico.  
  
 [N] '*command_string*'  
 É uma cadeia de caracteres constante que contém o comando a ser passado ao servidor vinculado. Se N for incluído, a cadeia de caracteres será interpretada como o tipo de dados **nvarchar**.  
  
 [?]  
 Indica parâmetros para os quais valores são fornecidos na \<arg-list> de comandos de passagem usados em uma instrução EXEC('...', \<arg-list>) AT \<linkedsrv>.  
  
 AT *linked_server_name*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica que *command_string* é executada em *linked_server_name* e os resultados, se houver, são retornados ao cliente. *linked_server_name* deve referenciar uma definição de servidor vinculado existente no servidor local. Os servidores vinculados são definidos por meio de [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 WITH \<execute_option>  
 Opções de execução possíveis. As opções de RESULT SETS não podem ser especificadas em uma instrução INSERT...EXEC.  
 
AT DATA_SOURCE data_source_name **Aplica-se a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e posterior
  
 Especifica que a *command_string* é executada no *data_source_name* e os resultados, se houver, são retornados ao cliente. *data_source_name* deve se referir a uma definição de EXTERNAL DATA SOURCE no banco de dados. Somente as fontes de dados que apontam para o SQL Server são compatíveis. Além disso, para as fonte de dados de cluster de Big Data do SQL Server que apontam para pool de computação, o pool de dados ou o pool de armazenamento são compatíveis. As fontes de dados são definidas usando [CREATE EXTERNAL DATA SOURCE](../statements/create-external-data-source-transact-sql.md).  
  
 WITH \<execute_option>  
 Opções de execução possíveis. As opções de RESULT SETS não podem ser especificadas em uma instrução INSERT...EXEC.  
  
|Termo|Definição|  
|----------|----------------|  
|RECOMPILE|Força a compilação, a utilização e o descarte de um novo plano após a execução do módulo. Se houver um plano de consulta existente para o módulo, esse plano permanecerá no cache.<br /><br /> Use essa opção se o parâmetro sendo fornecido for atípico ou se os dados tiverem sido alterados significativamente. Ela não é usada para procedimentos armazenados estendidos. É aconselhável usar essa opção se realmente for necessário porque ela é expansiva.<br /><br /> **Observação:** Não é possível usar WITH RECOMPILE ao chamar um procedimento armazenado que usa a sintaxe OPENDATASOURCE. A opção WITH RECOMPILE será ignorada quando um nome de objeto de quatro partes for especificado.<br /><br /> **Observação:** RECOMPILE não é compatível com funções escalares definidas pelo usuário compiladas nativamente. Se precisar recompilar, use [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md).|  
|**RESULT SETS UNDEFINED**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Esta opção não fornece nenhuma garantia de quais resultados, se houver, serão retornados. Além disso, não é fornecida nenhuma definição. A instrução é executada sem erro se algum resultado for retornado ou se nenhum resultado for retornado. RESULT SETS UNDEFINED será o comportamento padrão se não for fornecido result_sets_option.<br /><br /> Para funções escalares interpretadas definidas pelo usuário e funções escalares compiladas nativamente definidas pelo usuário, essa opção não funciona porque as funções nunca retornam um conjunto de resultados.|  
|RESULT SETS NONE|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Garante que a instrução execute não retornará nenhum resultado. Se algum resultado for retornado, o lote será anulado.<br /><br /> Para funções escalares interpretadas definidas pelo usuário e funções escalares compiladas nativamente definidas pelo usuário, essa opção não funciona porque as funções nunca retornam um conjunto de resultados.|  
|*\<result_sets_definition>*|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Fornece uma garantia de que o resultado voltará como especificado em result_sets_definition. Para instruções que retornam vários conjuntos de resultados, forneça várias seções de *result_sets_definition*. Coloque cada *result_sets_definition* entre parênteses, separada por vírgulas. Para obter mais informações, confira \<result_sets_definition> mais adiante neste tópico.<br /><br /> Essa opção sempre resulta em um erro para funções escalares definidas pelo usuário compiladas nativamente, porque as funções não retornam um conjunto de resultados.|
  
\<result_sets_definition>
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 Descreve os conjuntos de resultados retornados pelas instruções executadas. As cláusulas de result_sets_definition têm o seguinte significado  
  
|Termo|Definição|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124; NOT NULL]<br /><br /> }|Veja a tabela abaixo.|  
|db_name|O nome do banco de dados que contém a tabela, a exibição ou a função com valor de tabela.|  
|schema_name|O nome do esquema proprietário da tabela, da exibição ou da função com valor de tabela.|  
|table_name &#124; view_name &#124; table_valued_function_name|Especifica que as colunas retornadas serão as especificadas na tabela, exibição ou função com valor de tabela nomeada. Não há suporte para variáveis de tabela, tabelas temporárias e sinônimos na sintaxe de objetos do AS.|  
|AS TYPE [schema_name.]table_type_name|Especifica que as colunas retornadas serão as especificadas no tipo de tabela.|  
|AS FOR XML|Especifica que os resultados XML da instrução ou procedimento armazenado chamado pela instrução EXECUTE serão convertidos no formato como se fossem gerados por uma instrução SELECT ... FOR XML ... Toda a formatação das políticas do tipo na instrução original é removida, e os resultados são retornados como se nenhuma política do tipo fosse especificada. AS FOR XML não converte em XML os resultados de tabela não XML da instrução executada ou do procedimento armazenado.|  
  
|Termo|Definição|  
|----------|----------------|  
|column_name|Os nomes de cada coluna. Se o número de colunas for diferente do conjunto de resultados, ocorrerá um erro e o lote será anulado. Se o nome de uma coluna for diferente do conjunto de resultados, o nome de coluna retornado será definido como o nome definido.|  
|data_type|Os tipos de dados de cada coluna. Se os tipos de dados forem diferentes, será executada uma conversão implícita para o tipo de dados definido. Se a conversão falhar, o lote será anulado|  
|COLLATE collation_name|A ordenação de cada coluna. Se houver uma incompatibilidade de ordenação, será tentada uma ordenação implícita. Se isso falhar, o lote será anulado.|  
|NULL &#124; NOT NULL|A nulidade de cada coluna. Se a nulidade definida for NOT NULL e os dados retornados contiver NULLs, ocorrerá um erro e o lote será anulado. Se não especificado, o valor padrão se conforma à configuração das opções do ANSI_NULL_DFLT_ON e ANSI_NULL_DFLT_OFF.|  
  
 O conjunto de resultados real retornado durante execução pode diferir do resultado definido usando a cláusula WITH RESULT SETS de uma das seguintes maneiras: número de conjuntos de resultados, número de colunas, nome de coluna, nulidade e tipo de dados. Se o número de conjuntos de resultados for diferente, ocorrerá um erro e o lote será anulado.  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros podem ser fornecidos com *value* ou @*parameter_name*=*value*. . Um parâmetro não faz parte de uma transação; portanto, se um parâmetro for alterado em uma transação que for posteriormente revertida, o parâmetro não será revertido para seu valor anterior. O valor retornado ao chamador será sempre o valor no momento do retorno do módulo.  
  
 O aninhamento ocorre quando um módulo chama outro ou executa código gerenciado, fazendo referência a um módulo CLR (Common Language Runtime) a um tipo definido pelo usuário ou agregação. O nível de aninhamento é aumentado quando o módulo chamado ou a referência de código gerenciado inicia a execução e diminuído quando ela termina. Exceder o máximo de 32 níveis de aninhamento faz com que toda a cadeia de chamada falhe. O nível de aninhamento atual é armazenado na função do sistema @@NESTLEVEL.  
  
 Como os procedimentos armazenados remotos e estendidos não estão no escopo de uma transação (a menos que emitidos em uma instrução BEGIN DISTRIBUTED TRANSACTION ou quando usados com várias opções de configuração), os comandos executados por meio de chamadas a eles não poderão ser revertidos. Para obter mais informações, consulte [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) e [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Ao utilizar variáveis de cursor, se você executar um procedimento que passe em uma variável de cursor com um cursor alocado a ele, ocorrerá um erro.  
  
 Não é necessário especificar a palavra-chave EXECUTE durante a execução de módulos se a instrução for a primeira em um lote.  
  
 Para obter informações adicionais específicas de procedimentos armazenados CLR, consulte Procedimentos armazenados CLR.  
  
## <a name="using-execute-with-stored-procedures"></a>Usando EXECUTE com procedimentos armazenados  
 Não será preciso especificar a palavra-chave EXECUTE durante a execução de procedimentos armazenados quando a instrução for a primeira em um lote.  
  
 Procedimentos armazenados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciam com os caracteres sp_. Eles estão fisicamente armazenados no [banco de dados Resource](../../relational-databases/databases/resource-database.md), mas são exibidos logicamente no esquema sys de cada sistema e banco de dados definido pelo usuário. Quando você executa um procedimento armazenado de sistema, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com o nome do esquema sys.  
  
 Os procedimentos armazenados estendidos de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciam com os caracteres xp_ e estão contidos no esquema dbo do banco de dados mestre. Quando você executa um procedimento armazenado estendido de sistema, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com master.dbo.  
  
 Quando você executa um procedimento definido pelo usuário, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com um nome de esquema. Não recomendamos nomear um procedimento armazenado definido pelo usuário com o mesmo nome de uma procedimento armazenado no sistema. Para obter mais informações sobre a execução de procedimentos armazenados, consulte [Executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
## <a name="using-execute-with-a-character-string"></a>Usando EXECUTE com uma cadeia de caracteres  
 Em versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as cadeias de caracteres estão limitadas a 8.000 bytes. Isso requer a concatenação de cadeias de caracteres grandes para execução dinâmica. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os tipos de dados **varchar(max)** e **nvarchar(max)** podem ser especificados para permitir que as cadeias de caracteres tenham até 2 gigabytes de dados.  
  
 As alterações no contexto de banco de dados duram apenas até o fim da instrução EXECUTE. Por exemplo, depois que `EXEC` na instrução seguinte é executado, o contexto de banco de dados se torna o mestre.  
  
```sql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>Alternância de contexto  
 Você pode usar a cláusula `AS { LOGIN | USER } = ' name '` para alternar o contexto de execução de uma instrução dinâmica. Quando a alternância de contexto for especificada como `EXECUTE ('string') AS <context_specification>`, a duração dessa alternância estará limitada ao escopo da consulta sendo executada.  
  
###  <a name="specifying-a-user-or-login-name"></a><a name="_user"></a> Especificando um nome de logon ou usuário  
 O nome de logon ou de usuário especificado em `AS { LOGIN | USER } = ' name '` deve existir como principal em sys.database_principals ou sys.server_principals, respectivamente, ou a instrução falhará. Além disso, as permissões IMPERSONATE devem ser concedidas na entidade de segurança. A menos que o chamador seja o proprietário do banco de dados ou membro da função de servidor fixa sysadmin, o principal deverá existir quando o usuário estiver acessando o banco de dados ou a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma associação de grupo do Windows. Por exemplo, considere as seguintes condições:  
  
-   O grupo CompanyDomain\SQLUsers tem acesso ao banco de dados de vendas.  
  
-   CompanyDomain\SqlUser1 é membro de SQLUsers e, por isso, tem acesso implícito ao banco de dados de vendas.  
  
 Embora CompanyDomain\SqlUser1 tenha acesso ao banco de dados por meio da associação ao grupo SQLUsers, a instrução `EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'` falhará porque `CompanyDomain\SqlUser1` não existe como uma entidade de segurança no banco de dados.  
  
### <a name="best-practices"></a>Práticas Recomendadas  
 Especifique um logon ou um usuário que tenha os privilégios mínimos necessários para executar as operações definidas na instrução ou módulo. Por exemplo, não especifique um nome de logon que tenha permissões em nível de servidor se apenas as permissões em nível de banco de dados forem necessárias; ou não especifique uma conta de proprietário de banco de dados, a menos que essas permissões sejam solicitadas.  
  
## <a name="permissions"></a>Permissões  
 Não são solicitadas permissões para executar a instrução EXECUTE. Porém, são solicitadas permissões nos protegíveis mencionados na cadeia de caracteres EXECUTE. Por exemplo, se a cadeia de caracteres tiver uma instrução INSERT, o chamador da instrução EXECUTE deverá ter a permissão INSERT na tabela de destino. As permissões são verificadas quando a instrução EXECUTE for encontrada, mesmo se ela estiver incluída em um módulo.  
  
 As permissões EXECUTE de um padrão de módulo para o proprietário do módulo, que pode transferi-las a outros usuários. Quando um módulo que executa uma cadeia de caracteres é executado, as permissões são verificadas no contexto do usuário que executa o módulo e não no contexto do usuário que o criou. Entretanto, se o mesmo usuário for proprietário do módulo chamador e do módulo sendo chamado, a verificação da permissão EXECUTE não será feita para o segundo módulo.  
  
 Se o módulo acessar outros objetos de banco de dados, a execução ocorrerá quando a permissão EXECUTE estiver no módulo e uma das seguintes condições for verdadeira:  
  
-   O módulo está marcado como EXECUTE AS USER ou SELF, e o seu proprietário tem as permissões correspondentes no objeto mencionado. Para obter mais informações sobre a representação dentro de um módulo, consulte [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
-   O módulo está marcado como EXECUTE AS CALLER e você tem as permissões correspondentes no objeto.  
  
-   O módulo está marcado como EXECUTE AS *user_name*, e *user_name* tem as permissões correspondentes no objeto.  
  
### <a name="context-switching-permissions"></a>Permissões de alternância de contexto  
 Para especificar EXECUTE AS em um logon, o chamador precisa ter permissões IMPERSONATE no nome de logon especificado. Para especificar EXECUTE AS em um usuário de banco de dados, o chamador precisa ter permissões IMPERSONATE no nome de usuário especificado. Quando nenhum contexto de execução é especificado ou EXECUTE AS CALLER é especificado, as permissões de IMPERSONATE não são solicitadas.  
  
## <a name="examples-sql-server"></a>Exemplos: SQL Server
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>a. Usando EXECUTE para passar um único parâmetro  
 O procedimento armazenado `uspGetEmployeeManagers` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] espera um parâmetro (`@EmployeeID`). Os exemplos a seguir executam o procedimento armazenado `uspGetEmployeeManagers` com `Employee ID 6` como seu valor de parâmetro.  
  
```sql    
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 A variável pode ser nomeada explicitamente na execução:  
  
```sql    
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 Se o exemplo a seguir for a primeira instrução de um lote ou em um script **osql** ou **sqlcmd**, EXEC não será obrigatório.  
  
```sql    
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. Usando vários parâmetros  
 O exemplo a seguir executa o procedimento armazenado `spGetWhereUsedProductID` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Ele passa dois parâmetros: o primeiro é uma identificação de produto (`819`) e o segundo `@CheckDate,` é um valor `datetime`.  
  
```sql    
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsql_string-with-a-variable"></a>C. Usando EXECUTE 'tsql_string' com uma variável  
 O exemplo seguinte mostra como `EXECUTE` controla dinamicamente as cadeias de caracteres criadas que contêm variáveis. Esse exemplo cria o cursor `tables_cursor` para manter uma lista de todas as tabelas definidas pelo usuário no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, depois, usa essa lista para criar novamente todos os índices nas tabelas.  
  
```sql    
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. Usando EXECUTE com um procedimento armazenado remoto  
 O exemplo a seguir executa o procedimento `uspGetEmployeeManagers` armazenado no servidor remoto `SQLSERVER1` e armazena o status de retorno que indica o êxito ou a falha em `@retstat`.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```sql    
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. Usando EXECUTE com uma variável de procedimento armazenado  
 O exemplo seguinte cria uma variável que representa um nome de procedimento armazenado.  
  
```sql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. Usando EXECUTE com DEFAULT  
 O exemplo seguinte cria um procedimento armazenado com valores padrão para o primeiro e terceiro parâmetros. Quando o procedimento é executado, esses padrões serão inseridos para o primeiro e terceiro parâmetros quando nenhum valor for informado na chamada ou quando o padrão for especificado. Observe os vários modos que a palavra-chave `DEFAULT` pode ser usada.  
  
```sql    
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 O procedimento armazenado `Proc_Test_Defaults` pode ser executado em muitas combinações.  
  
```sql    
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linked_server_name"></a>G. Usando EXECUTE com AT linked_server_name  
 O exemplo seguinte envia uma cadeia de caracteres de comando a um servidor remoto. Ele cria um servidor vinculado `SeattleSales` que aponta para outra instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa uma instrução DDL (`CREATE TABLE`) nesse servidor vinculado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```sql    
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. Usando EXECUTE WITH RECOMPILE  
 O exemplo a seguir executa o procedimento armazenado `Proc_Test_Defaults` e força a compilação, o uso e o descarte de um novo plano de consulta após a execução do módulo.  
  
```sql    
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>I. Usando EXECUTE com uma função definida pelo usuário  
 O exemplo a seguir executa a função escalar definida pelo usuário `ufnGetSalesOrderStatusText` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. É utilizada a variável `@returnstatus` para armazenar o valor retornado pela função. A função espera um parâmetro de entrada, `@Status`. Isso é definido como um tipo de dados **tinyint**.  
  
```sql    
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. Usando EXECUTE para consultar um banco de dados Oracle em um servidor vinculado  
 O exemplo a seguir executa várias instruções `SELECT` no servidor remoto Oracle. O exemplo começa adicionando o servidor Oracle como um servidor vinculado e criando o logon de servidor vinculado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```sql    
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>K. Usando EXECUTE AS USER para alternar o contexto para outro usuário  
 O exemplo a seguir executa uma cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)] que cria uma tabela e especifica a cláusula `AS USER` para alternar o contexto de execução da instrução do chamador para `User1`. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará as permissões de `User1` quando a instrução for executada. `User1` deve existir como um usuário no banco de dados e deve ter permissão para criar tabelas no esquema `Sales`, caso contrário, haverá falha na instrução.  
  
```sql    
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linked_server_name"></a>L. Usando um parâmetro com EXECUTE e AT linked_server_name  
 O exemplo a seguir envia uma cadeia de caracteres de comando a um servidor remoto usando um ponto de interrogação (`?`) como espaço reservado de um parâmetro. O exemplo cria um servidor vinculado `SeattleSales` que aponta para outra instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa uma instrução `SELECT` nesse servidor vinculado. A instrução `SELECT` usa o ponto de interrogação como um espaço reservado para o parâmetro `ProductID` (`952`), fornecido após a instrução.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```sql    
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>M. Usando EXECUTE para redefinir um único conjunto de resultados  
 Alguns dos exemplos anteriores executaram `EXEC dbo.uspGetEmployeeManagers 6;` que retornou 7 colunas. O exemplo a seguir demonstra o uso da sintaxe `WITH RESULT SET` para alterar os nomes e tipos de dados do conjunto de resultados retornado.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```sql    
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>N. Usando EXECUTE para redefinir dois conjuntos de resultados  
 Ao executar uma instrução que retorna mais de um conjunto de resultados, defina cada conjunto de resultados esperado. O exemplo a seguir em [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] cria um procedimento armazenado que retorna dois conjuntos de resultados. Em seguida, o procedimento é executado com a cláusula **WITH RESULT SETS** e com a especificação definições de dois conjuntos de resultados.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```sql    
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  ### <a name="o-using-execute-with-at-data_source-data_source_name-to-query-a-remote-sql-server"></a>O. Usando EXECUTE com AT DATA_SOURCE data_source_name para consultar um SQL Server remoto 
  
 O exemplo a seguir passa uma cadeia de caracteres de comando para uma fonte de dados externa apontando para uma Instância do SQL Server. 
  
**Aplica-se a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e posterior
  
```sql    
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE my_sql_server;  
GO  
```  
  
### <a name="p-using-execute-with-at-data_source-data_source_name-to-query-compute-pool-in-sql-server-big-data-cluster"></a>P. Usando EXECUTE com AT DATA_SOURCE data_source_name para consultar um pool de computação no Cluster de Big Data do SQL Server 

 O exemplo a seguir passa uma cadeia de caracteres de comando para uma fonte de dados externa apontando para um pool de computação no Cluster de Big Data do SQL Server. O exemplo cria uma fonte de dados `SqlComputePool` em um pool de computação no Cluster de Big Data do SQL Server e executa uma instrução `SELECT` na fonte de dados. 
  
**Aplica-se a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e posterior
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlComputePool 
WITH (LOCATION = 'sqlcomputepool://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlComputePool;  
GO  
```  

### <a name="q-using-execute-with-at-data_source-data_source_name-to-query-data-pool-in-sql-server-big-data-cluster"></a>Q. Usando EXECUTE com AT DATA_SOURCE data_source_name para consultar um pool de dados no Cluster de Big Data do SQL Server 
 O exemplo a seguir passa uma cadeia de caracteres de comando para uma fonte de dados externa apontando para um pool de computação no cluster de Big Data do SQL Server. O exemplo cria uma fonte de dados `SqlDataPool` em um pool de dados no cluster de Big Data do SQL Server e executa uma instrução `SELECT` na fonte de dados. 
  
**Aplica-se a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e posterior
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlDataPool 
WITH (LOCATION = 'sqldatapool://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlDataPool;  
GO  
```

### <a name="r-using-execute-with-at-data_source-data_source_name-to-query-storage-pool-in-sql-server-big-data-cluster"></a>R. Usando EXECUTE com AT DATA_SOURCE data_source_name para consultar um pool de armazenamento no Cluster de Big Data do SQL Server 

 O exemplo a seguir passa uma cadeia de caracteres de comando para uma fonte de dados externa apontando para um pool de computação no Cluster de Big Data do SQL Server. O exemplo cria uma fonte de dados `SqlStoragePool` em um pool de dados no Cluster de Big Data do SQL Server e executa uma instrução `SELECT` na fonte de dados. 
  
**Aplica-se a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e posterior
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlStoragePool
WITH (LOCATION = 'sqlhdfs://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlStoragePool;  
GO  
```

  
## <a name="examples-azure-synapse-analytics"></a>Exemplos: Azure Synapse Analytics 
  
### <a name="a-basic-procedure-execution"></a>A: Execução de procedimento armazenado  
 Executando um procedimento armazenado:  
  
```sql  
EXEC proc1;  
```  
  
 Chamando um procedimento armazenado com um nome determinado em runtime:  
  
```sql    
EXEC ('EXEC ' + @var);  
```  
  
 Chamando um procedimento armazenado em um procedimento armazenado:  
  
```sql   
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="b-executing-strings"></a>B: Como executar cadeias de caracteres  
 Executando uma cadeia de caracteres SQL:  
  
```sql   
EXEC ('SELECT * FROM sys.types');  
```  
  
 Executando uma cadeia de caracteres aninhada:  
  
```sql  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 Executando uma variável de cadeia de caracteres:  
  
```sql  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="c-procedures-with-parameters"></a>C: Procedimentos com parâmetros  

 O seguinte exemplo cria um procedimento com parâmetros e demonstra três maneiras de executar o procedimento:  
  
```sql  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Utilitário osql](../../tools/osql-utility.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  
