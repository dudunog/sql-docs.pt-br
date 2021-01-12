---
description: SET @local_variable (Transact-SQL)
title: SET @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
author: cawrites
ms.author: chadam
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: caf0fcb2a9b00c8f391280395629348f055d4039
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100942"
---
# <a name="set-local_variable-transact-sql"></a>SET @local_variable (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Define a variável local especificada, criada anteriormente com a instrução DECLARE @*local_variable*, com o valor especificado.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
Sintaxe do SQL Server e do Banco de Dados SQL do Azure:

```syntaxsql
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
Sintaxe do Azure Synapse Analytics e do Parallel Data Warehouse:  
```syntaxsql
SET @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
**@** _local_variable_  
O nome de uma variável de qualquer tipo, exceto **cursor**, **text**, **ntext**, **image** ou **table**. Os nomes de variável devem começar com um sinal de arroba ( **@** ). Os nomes de variável precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
*property_name*  
Uma propriedade de um tipo definido pelo usuário.  
  
*field_name*  
Um campo público de um tipo definido pelo usuário.  
  
*udt_name*  
O nome de um tipo de dados CLR (Common Language Runtime) definido pelo usuário.  
  
`{ . | :: }`  
Especifica um método de um tipo de dados CLR definido pelo usuário. Para um método de instância (não estático), use um ponto (**.**). Para um método estático, use dois sinais de dois-pontos (**::**). Para invocar um método, uma propriedade ou um campo de um tipo de dados CLR definido pelo usuário, você deve ter a permissão EXECUTE no tipo.  
  
_method_name_ **(** _argument_ [ **,** ... *n* ] **)**  
Um método de um tipo definido pelo usuário que obtém um ou mais argumentos para modificar o estado de uma instância de um tipo. Os métodos estáticos devem ser públicos.  
  
**@** _SQLCLR_local_variable_  
Uma variável cujo tipo está localizado em um assembly. Para obter mais informações, consulte [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
*mutator_method*  
Um método no assembly que pode alterar o estado do objeto. SQLMethodAttribute.IsMutator é aplicado a este método.  
  
`{ += | -= | *= | /= | %= | &= | ^= | |= }`  
Operador de atribuição composto:  
  
 +=              Adicionar e atribuir  
  
 -=              Subtrair e atribuir  
  
 *=              Multiplicar e atribuir  
  
 /=              Dividir e atribuir  
  
 %=              Módulo e atribuir  
  
 &=              AND bit a bit e atribuir  
  
 ^=              XOR bit a bit e atribuir  
  
 |=              OR bit a bit e atribuir  
  
*expressão*  
Qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
*cursor_variable*  
O nome de uma variável de cursor. Se a variável de cursor de destino tiver mencionado anteriormente um cursor diferente, essa referência anterior será removida.  
  
*cursor_name*  
O nome de um cursor declarado usando a instrução DECLARE CURSOR.  
  
CURSOR  
Especifica que a instrução SET contém uma declaração de um cursor.  
  
SCROLL  
Especifica que o cursor oferece o suporte para todas as opções de busca: FIRST, LAST, NEXT, PRIOR, RELATIVE e ABSOLUTE. Não é possível especificar SCROLL quando também tiver especificado FAST_FORWARD.  
  
FORWARD_ONLY  
Especifica que o cursor oferece suporte somente para a opção FETCH NEXT. O cursor é recuperado somente em uma direção, da primeira para a última linha. Quando FORWARD_ONLY é especificado sem as palavras-chave STATIC, KEYSET ou DYNAMIC, o cursor é implementado como DYNAMIC. Se FORWARD_ONLY ou SCROLL não forem especificados, FORWARD_ONLY será o padrão, a não ser que as palavras-chave STATIC, KEYSET ou DYNAMIC sejam especificadas. Para os cursores STATIC, KEYSET e DYNAMIC, SCROLL é o padrão.  
  
STATIC  
Define um cursor que faz uma cópia temporária dos dados a serem usados por ele. Todas as solicitações para o cursor são respondidas dessa tabela temporária em tempdb. Como resultado, as modificações feitas nas tabelas base, depois que o cursor é aberto, não são refletidas nos dados retornados pelas buscas feitas para o cursor. E esse cursor não dá suporte a modificações.  
  
KEYSET  
Especifica que a associação e a ordem de linhas no cursor são fixas, quando o cursor é aberto. O conjunto de chaves que identifica exclusivamente as linhas é criado na tabela keysettable no tempdb. Alterações em valores não chave nas tabelas base, realizadas pelo proprietário do cursor ou confirmadas por outros usuários, são visíveis como rolagens do proprietário ao redor do cursor. As inserções feitas por outros usuários não são visíveis e não é possível fazer inserções por um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Se uma linha é excluída, uma tentativa de buscá-la retorna um @@FETCH_STATUS igual a -2. As atualizações de valores de chave externas ao cursor são similares à exclusão de uma linha antiga, seguida de uma inserção de uma nova linha. A linha com os novos valores não é visível e as tentativas de buscar a linha com os valores antigos retornam um @@FETCH_STATUS igual a -2. Os novos valores ficarão visíveis se a atualização for feita pelo cursor, especificando a cláusula WHERE CURRENT OF.  
  
DYNAMIC  
Define um cursor que reflete todas as mudanças de dados feitas nas linhas no seu conjunto de resultados conforme o proprietário rola o cursor. Os valores de dados, a ordem e a associação das linhas podem ser alterados em cada busca. As opções de busca absoluta e relativa não têm suporte em cursores dinâmicos.  
  
FAST_FORWARD  
Especifica um cursor FORWARD_ONLY, READ_ONLY, com otimizações habilitadas. FAST_FORWARD não pode ser especificado quando SCROLL também está especificado.  
  
READ_ONLY  
Impede que esse cursor faça atualizações. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
SCROLL LOCKS  
Especifica se atualizações posicionadas ou exclusões feitas pelo cursor têm garantia de êxito. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueia as linhas à medida que são lidas no cursor para garantir a disponibilidade para modificações posteriores. SCROLL_LOCKS não pode ser especificado quando FAST_FORWARD também está especificado.  
  
OPTIMISTIC  
Especifica que as atualizações posicionadas e exclusões realizadas pelo cursor não terão êxito se a linha tiver sido atualizada desde que foi lida no cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueia linhas à medida que são lidas no cursor. Em vez disso, ele usará comparações de valores da coluna de carimbo de data/hora ou um valor de soma de verificação, se a tabela não tiver nenhuma coluna de carimbo de data/hora, para determinar se a linha foi modificada depois de lida no cursor. Se a linha tiver sido modificada, a tentativa de atualização ou exclusão posicionada falhará. OPTIMISTIC não poderá ser especificado quando FAST_FORWARD também estiver especificado.  
  
TYPE_WARNING  
Especifica que uma mensagem de aviso é enviada ao cliente quando o cursor é convertido implicitamente em outro a partir do tipo solicitado.  
  
FOR *select_statement*  
É uma instrução SELECT padrão que define o conjunto de resultados de um cursor. As palavras-chave FOR BROWSE e INTO não são permitidas em *select_statement* de uma declaração de cursor.  
  
Se DISTINCT, UNION, GROUP BY ou HAVING forem usados ou uma expressão de agregação for incluída em *select_list*, o cursor será criado como STATIC.  
  
Se cada tabela subjacente não tiver um índice exclusivo e um cursor ISO SCROLL ou um cursor [!INCLUDE[tsql](../../includes/tsql-md.md)] KEYSET for solicitado, ele será automaticamente um cursor STATIC.  
  
Se *select_statement* contiver uma cláusula ORDER BY na qual as colunas não são identificadores de linha exclusivos, um cursor DYNAMIC será convertido em um cursor KEYSET ou em um cursor STATIC, caso não seja possível abrir um cursor KEYSET. Isto também acontece para um cursor definido usando a sintaxe ISO, mas sem a palavra-chave STATIC.  
  
READ ONLY  
Impede que esse cursor faça atualizações. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado. Essa palavra-chave é diferente do READ_ONLY anterior, pois tem um espaço em vez de um sublinhado entre READ e ONLY.  
  
`UPDATE [OF column_name[ ,... n ] ]`  
Define colunas atualizáveis em um cursor. Se OF *column_name* [**,**...*n*] for fornecido, somente as colunas listadas permitirão modificações. Quando nenhuma lista for fornecida, todas as colunas poderão ser atualizadas, a menos que o cursor tenha sido definido como READ_ONLY.  
  
## <a name="remarks"></a>Comentários  
Depois de uma variável ser declarada, ela é inicializada como NULL. Use a instrução SET para atribuir um valor que não é NULL a uma variável declarada. A instrução SET que atribui um valor à variável retorna um único valor. Ao inicializar várias variáveis, use uma instrução SET separada para cada variável local.  
  
As variáveis podem ser usadas somente em expressões, não em nomes de objeto ou palavras-chave. Para construir instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmicas, use EXECUTE.  
  
As regras de sintaxe para SET **@** _cursor_variable_ não incluem as palavras-chave LOCAL e GLOBAL. Quando a sintaxe SET **@** _cursor_variable_ = CURSOR... é usada, o cursor é criado como GLOBAL ou LOCAL, dependendo da configuração padrão da opção de banco de dados do cursor local.  
  
As variáveis de cursor sempre são locais, mesmo se fizerem referência a um cursor global. Quando uma variável de cursor faz referência a um cursor global, o cursor tem as duas referências, uma global e uma local. Para obter mais informações, veja o Exemplo C.  
  
Para obter mais informações, consulte [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
O operador de atribuição composto pode ser usado em qualquer lugar em que haja uma atribuição com uma expressão à direita do operador, incluindo variáveis, e uma instrução SET em uma instrução UPDATE, SELECT e RECEIVE.  
  
Não use uma variável em uma instrução SELECT para concatenar valores (ou seja, para computar valores agregados). Resultados inesperados de consulta podem ocorrer. Porque todas as expressões na lista SELECT (incluindo atribuições) não são necessariamente executadas exatamente uma vez para cada linha de saída. Para obter mais informações, consulte o [este artigo da base de dados](https://support.microsoft.com/kb/287515).  
  
## <a name="permissions"></a>Permissões  
Requer associação à função public. Todos os usuários podem usar SET **@** _local_variable_.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>a. Imprimindo o valor de uma variável inicializada com a instrução SET  
O exemplo a seguir cria a variável `@myvar`, coloca um valor de cadeia de caracteres na variável e imprime o valor da variável `@myvar`.  
  
```sql  
DECLARE @myvar CHAR(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>B. Usando uma variável local que atribuiu um valor usando a instrução SET em uma instrução SELECT  
O exemplo a seguir cria uma variável local chamada `@state` e usa essa variável local em uma instrução `SELECT` para localizar o nome e o sobrenome de todos os funcionários que moram no estado de `Oregon`.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @state CHAR(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. Usando uma atribuição composta para uma variável local  
Os dois exemplos a seguir produzem o mesmo resultado. Eles criam uma variável local chamada `@NewBalance`, multiplicam-na por 10 e exibem o novo valor da variável local em uma instrução `SELECT`. O segundo exemplo usa um operador de atribuição composto.  
  
```sql  
/* Example one */  
DECLARE  @NewBalance  INT ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance INT = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. Usando SET com um cursor global  
O exemplo a seguir cria uma variável local e define a variável de cursor como o nome de cursor global.  
  
```sql  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. Definindo um cursor com a instrução SET  
O exemplo a seguir usa a instrução `SET` para definir um cursor.  
  
```sql  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. Atribuindo um valor de uma consulta  
O exemplo a seguir usa uma consulta para atribuir um valor a uma variável.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @rows INT;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. Atribuindo um valor a uma variável de tipo definido pelo usuário com a modificação de uma propriedade do tipo  
O exemplo a seguir define o valor para o tipo `Point` definido pelo usuário modificando o valor da propriedade `X` do tipo.  
  
```sql  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. Atribuindo um valor a uma variável de tipo definida com a invocação de um método do tipo  
O exemplo a seguir define um valor para o tipo **point** definido pelo usuário por meio da invocação do método `SetXY` do tipo.  
  
```sql  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>I. Criando uma variável para um tipo CLR e chamando um método modificador  
O exemplo a seguir cria uma variável para o tipo `Point` e, depois, executa um método modificador em `Point`.  
  
```sql  
CREATE ASSEMBLY mytest FROM 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. Imprimindo o valor de uma variável inicializada com a instrução SET  
O exemplo a seguir cria a variável `@myvar`, coloca um valor de cadeia de caracteres na variável e imprime o valor da variável `@myvar`.  
  
```sql  
DECLARE @myvar CHAR(20);  
SET @myvar = 'This is a test';  
SELECT TOP 1 @myvar FROM sys.databases;
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>K. Usando uma variável local que atribuiu um valor usando a instrução SET em uma instrução SELECT  
O exemplo a seguir cria uma variável local chamada `@dept` e usa essa variável em uma instrução `SELECT` para localizar o nome e o sobrenome de todos os funcionários que trabalham no departamento `Marketing`.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @dept CHAR(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>L. Usando uma atribuição composta para uma variável local  
Os dois exemplos a seguir produzem o mesmo resultado. Eles criam uma variável local chamada `@NewBalance`, multiplicam-na por `10` e exibem o novo valor da variável local em uma instrução `SELECT`. O segundo exemplo usa um operador de atribuição composto.  
  
```sql  
/* Example one */  
DECLARE  @NewBalance INT;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance INT = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>M. Atribuindo um valor de uma consulta  
O exemplo a seguir usa uma consulta para atribuir um valor a uma variável.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @rows INT;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>Consulte Também  
[Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
[Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

