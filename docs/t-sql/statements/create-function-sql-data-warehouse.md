---
title: CREATE FUNCTION (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
author: juliemsft
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ae8c2994e43ff6a90105dd39c203a455da2c9468
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196764"
---
# <a name="create-function-sql-data-warehouse"></a>CREATE FUNCTION (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Cria uma função definida pelo usuário no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Uma função definida pelo usuário é uma rotina [!INCLUDE[tsql](../../includes/tsql-md.md)] que aceita parâmetros, executa uma ação, como um cálculo complexo, e retorna o resultado dessa ação como um valor. O valor retornado deve ser um valor escalar (único). Use essa instrução para criar uma rotina reutilizável que possa ser usada destas maneiras:  
  
-   Em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como SELECT  
  
-   Em aplicativos que chamam a função  
  
-   Na definição de outra função definida pelo usuário  
  
-   Para definir uma restrição CHECK em uma coluna  
  
-   Para substituir um procedimento armazenado  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *function_name*  
 É o nome da função definida pelo usuário. Os nomes de funções devem obedecer às regras de identificadores e devem ser exclusivos dentro do banco de dados e em seu esquema.  
  
> [!NOTE]  
>  São necessários parênteses depois do nome de função mesmo que um parâmetro não seja especificado.  
  
 @*parameter_name*  
 É um parâmetro na função definida pelo usuário. Podem ser declarados um ou mais parâmetros.  
  
 Uma função pode ter no máximo 2.100 parâmetros. O valor de cada parâmetro declarado deve ser fornecido pelo usuário quando a função é executada, a menos que seja definido um padrão para o parâmetro.  
  
 Especifique um nome de parâmetro usando um sinal de arroba (@) como o primeiro caractere. O nome do parâmetro deve estar em conformidade com as regras de identificadores. Os parâmetros são locais para a função. Os mesmos nomes de parâmetro podem ser usados em outras funções. Os parâmetros só podem assumir o lugar de constantes. Eles não podem ser usados no lugar de nomes de tabela, nomes de coluna ou nomes de outros objetos de banco de dados.  
  
> [!NOTE]  
>  ANSI_WARNINGS não é cumprido quando você passa parâmetros em um procedimento armazenado, em uma função definida pelo usuário ou quando declara ou define variáveis em uma instrução de lote. Por exemplo, se a variável for definida como **char(3)** e, em seguida, configurada com um valor maior que três caracteres, os dados serão truncados até o tamanho definido e a instrução INSERT ou UPDATE terá êxito.  
  
 *parameter_data_type*  
 É o tipo de dados de parâmetro. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados escalares compatíveis com o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] são permitidos. O tipo de dados de carimbo de data/hora (rowversion) não é um tipo compatível.  
  
 [ =*default* ]  
 É um valor padrão para o parâmetro. Se um valor *default* for definido, a função poderá ser executada sem a necessidade de especificar um valor para esse parâmetro.  
  
 Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deverá ser especificada quando a função for chamada para recuperar o valor padrão. Esse comportamento é diferente do uso de parâmetros com valores padrão em procedimentos armazenados nos quais a omissão do parâmetro também indica o valor padrão.  
  
 *return_data_type*  
 É o valor de retorno de uma função escalar definida pelo usuário. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados escalares compatíveis com o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] são permitidos. O tipo de dados de carimbo de data/hora (rowversion) não é um tipo compatível. Os tipos não escalares de cursor e tabela não são permitidos.  
  
 *function_body*  
 Série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  O function_body não pode conter uma instrução SELECT e não pode referenciar os dados do banco de dados.  O function_body não pode referenciar tabelas nem exibições. O corpo da função pode chamar outras funções determinísticas, mas não pode chamar funções não determinísticas. 
  
 Em funções escalares, *function_body* é uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que juntas são avaliadas para um valor escalar.  
  
 *scalar_expression*  
 Especifica o valor escalar que a função escalar retorna.  
  
 **\<function_option>::=** 
  
 Especifica que a função terá uma ou mais das opções a seguir.  
  
 SCHEMABINDING  
 Especifica que a função está associada aos objetos de banco de dados referenciados por ela. Quando SCHEMABINDING for especificado, os objetos base não poderão ser modificadas de um modo que possa afetar a definição da função. A própria definição da função deve ser primeiro modificada ou descartada para remover as dependências no objeto a ser modificado.  
  
 A associação da função aos objetos referenciados por ela será removida somente quando ocorrer uma das ações a seguir:  
  
-   A função for descartada.  
  
-   A função for modificada com o uso da instrução ALTER sem a especificação da opção SCHEMABINDING.  
  
 Uma função poderá ser associada a esquemas apenas se as condições a seguir forem verdadeiras:  
  
-   As funções definidas pelo usuário referenciadas pela função também são associadas a esquema.  
  
-   As funções e outras UDFs referenciadas pela função são referenciadas usando um nome de uma ou duas partes.  
  
-   Somente funções internas e outras UDFs no mesmo banco de dados podem ser referenciadas no corpo de UDFs.  
  
-   O usuário que executou a instrução CREATE FUNCTION tem permissão REFERENCES nos objetos do banco de dados referidos pela função.  
  
 Para remover SCHEMABINDING, use ALTER  
  
 RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
 Especifica o atributo **OnNULLCall** de uma função de valor escalar. Se não for especificado, CALLED ON NULL INPUT será implícito por padrão. Isso significa que o corpo da função será executado mesmo que NULL seja passado como um argumento.  
  
## <a name="best-practices"></a>Práticas Recomendadas  
 Se uma função definida pelo usuário não for criada com a cláusula SCHEMABINDING, as alterações feitas nos objetos subjacentes poderão afetar a definição da função e produzir resultados inesperados quando ela for chamada. É recomendável que você implemente um dos seguintes métodos para garantir que a função não se torne desatualizada devido a alterações em seus objetos subjacentes:  
  
-   Especifique a cláusula WITH SCHEMABINDING quando estiver criando a função. Isso garante que os objetos referenciados na definição da função não possam ser modificados, a menos que a função também seja modificada.  
  
## <a name="interoperability"></a>Interoperabilidade  
 As instruções a seguir são válidas em uma função:  
  
-   Instruções de atribuição.  
  
-   Instruções de controle de fluxo com exceção das instruções TRY...CATCH.  
  
-   Instruções DECLARE que definem variáveis de dados locais.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Funções definidas pelo usuário não podem ser usadas para executar ações que modificam o estado do banco de dados.  
  
 Funções definidas pelo usuário podem ser aninhadas, isto é, uma função definida pelo usuário pode chamar outra. O nível de aninhamento é incrementado quando a execução da função é iniciada, e reduzido quando a execução da função chamada é concluída. Até 32 níveis de funções definidas pelo usuário podem ser aninhados. Se o máximo de níveis de aninhamento for excedido haverá falha em toda a cadeia de funções da chamada de aninhamento.   
  
## <a name="metadata"></a>Metadados  
 Esta seção lista as exibições do catálogo do sistema que podem ser usadas para retornar metadados sobre funções definidas pelo usuário.  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) : exibe a definição de funções definidas pelo usuário [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo:  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : Exibe informações sobre os parâmetros definidos em funções definidas pelo usuário.  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : Exibe os objetos subjacentes referenciados por uma função.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE FUNCTION no banco de dados e a permissão ALTER no esquema no qual a função está sendo criada.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>a. Usando uma função com valor escalar definida pelo usuário para alterar um tipo de dados  
 Essa função simples usa um tipo de dados **int** como uma entrada e retorna um tipo de dados **decimal(10,2)** como uma saída.  
  
```sql  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FUNCTION (SQL Server PDW)](https://msdn.microsoft.com/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [DROP FUNCTION (SQL Server PDW)](https://msdn.microsoft.com/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  


