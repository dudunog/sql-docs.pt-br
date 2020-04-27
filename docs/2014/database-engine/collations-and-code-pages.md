---
title: Agrupamentos e páginas de código | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1969a3e30b31a21c380559a3e8898f87eb8848b1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786731"
---
# <a name="collations-and-code-pages"></a>Páginas de código de ordenações
  O [!INCLUDE[hek_2](../includes/hek-2-md.md)] tem restrições nas páginas de código com suporte para colunas (var)char em tabelas com otimização de memória e ordenações com suporte usados em índices e em procedimentos armazenados compilados nativamente.  
  
 A página de código para um valor (var)char determina o mapeamento entre caracteres e a representação de bytes que é armazenada na tabela. Por exemplo, com a página de código Latin 1 do Windows (1252; o padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), o caractere 'a' corresponde ao byte 0x61.  
  
 A página de código do valor (var)char é determinada pela ordenação associada ao valor. Por exemplo, a ordenação SQL_Latin1_General_CP1_CI_AS tem a página de código associada 1252.  
  
 A ordenação de um valor é herdada da ordenação de banco de dados ou pode ser especificada explicitamente usando a palavra-chave COLLATE. A ordenação de banco de dados não poderá ser alterada se o banco de dados contiver tabelas com otimização de memória ou procedimentos armazenados nativamente compilados. O exemplo a seguir define a ordenação de banco de dados e cria uma tabela, que tem uma coluna com uma ordenação diferente. O banco de dados usa a ordenação Latin que não diferencia maiúsculas de minúsculas.  
  
 Os índices só poderão ser criados em colunas de cadeia de caracteres se usarem uma ordenação BIN2. A variável LastName usa a ordenação BIN2. FirstName usa o padrão de banco de dados, que é CI_AS (sem diferenciação de maiúsculas e minúsculas, com diferenciação de acentos).  
  
> [!IMPORTANT]  
>  Você não pode usar ordenar por ou agrupar por em colunas de cadeia de caracteres de índice que não utilizem a ordenação BIN2.  
  
```sql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 As seguintes restrições se aplicam a tabelas com otimização de memória e a procedimentos armazenados compilados nativamente:  
  
-   As colunas (var)char em tabelas com otimização de memória devem usar ordenação 1252 de página de código. Essa restrição não se aplica às colunas n(var)char. O código a seguir recupera todas as ordenações 1252:  
  
    ```sql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     Se você precisar armazenar caracteres não latinos, use colunas n(var)char.  
  
-   Índices nas colunas (n)(var)char só podem ser especificados com ordenações BIN2 (veja o primeiro exemplo). A consulta a seguir recupera todas as ordenações BIN2 com suporte:  
  
    ```sql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     Ao acessar a tabela pelo [!INCLUDE[tsql](../includes/tsql-md.md)]interpretado, você pode usar a palavra-chave `COLLATE` para alterar a ordenação com expressões ou operações de classificação. Consulte o último exemplo para obter uma amostra disso.  
  
-   Os procedimentos armazenados nativamente compilados não podem usar parâmetros, variáveis locais ou constantes de cadeia de caracteres do tipo (var)char se a ordenação de banco de dados não for uma ordenação 1252 de página de código.  
  
-   Todas as expressões e operações de classificação dentro dos procedimentos armazenados compilados nativamente devem usar ordenações BIN2. A implicação é que todas as comparações e operações de classificação são baseadas nos pontos de código Unicode dos caracteres (representações binárias). Por exemplo, todas as classificações diferenciam maiúsculas de minúsculas ('Z' vem antes de 'a'). Se necessário, use [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado para classificação e comparação sem diferenciação de maiúsculas e minúsculas.  
  
-   O truncamento de dados UTF-16 não tem suporte dentro de procedimentos armazenados compilados nativamente. Isso significa que n (var) valores de Char (*n*) não podem ser convertidos para o tipo n (var) Char (*i*), se *eu* < *n*, se o agrupamento tiver a propriedade _SC. Por exemplo, o seguinte não tem suporte:  
  
    ```sql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     As funções de manipulação de cadeia de caracteres, como LEN, SUBSTRING, LTRIM e RTRIM com dados UTF-16 não têm suporte dentro de procedimentos armazenados compilados nativamente. Não é possível usar essas funções de manipulação de cadeia de caracteres para os valores de n(var)char que têm uma ordenação _SC.  
  
     Declare variáveis usando os tipos que são grandes o suficiente para impedir o truncamento.  
  
 O exemplo a seguir mostra algumas das implicações e soluções alternativas para as limitações de ordenação na OLTP na memória. O exemplo usa a tabela Employees especificada acima. Este exemplo lista todos os funcionários. Observe que para LastName, devido à ordenação primária, os nomes em letras maiúsculas são classificados antes daqueles com letras minúsculas. Consequentemente, 'Thomas' vem antes de 'nolan' porque os caracteres maiúsculos têm pontos de código inferiores. FirstName tem uma ordenação sem diferenciação de maiúsculas e minúsculas. Desse modo, a classificação é por ordem alfabética, e não pelo ponto de código dos caracteres.  
  
```sql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
