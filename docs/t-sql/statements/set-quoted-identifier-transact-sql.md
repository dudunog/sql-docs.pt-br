---
description: SET QUOTED_IDENTIFIER (Transact-SQL)
title: SET QUOTED_IDENTIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 232c287564593eee0deab4ae37dc13c36d2d689b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100731"
---
# <a name="set-quoted_identifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga as regras ISO relativas às aspas que delimitam identificadores e cadeias de caracteres literais. Identificadores delimitados por aspas duplas podem ser palavras-chave reservadas [!INCLUDE[tsql](../../includes/tsql-md.md)] ou podem conter caracteres que nem sempre são permitidos pelas regras da sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server, Azure SQL Database and serverless SQL pool in Azure Synapse Analytics

SET QUOTED_IDENTIFIER { ON | OFF }
```

```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse

SET QUOTED_IDENTIFIER ON
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
Quando `SET QUOTED_IDENTIFIER` for ON (padrão), os identificadores podem ser delimitados por aspas duplas (" "), e os literais precisam ser delimitados por aspas simples (' '). Todas as cadeias de caracteres delimitadas por aspas duplas são interpretadas como identificadores de objeto. Portanto identificadores entre aspas não precisam seguir as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Elas podem ser palavras-chave reservadas e incluir caracteres geralmente não permitidos nos identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aspas duplas não podem ser usadas para delimitar expressões de cadeias de caracteres literais. Aspas simples devem ser usadas para delimitar cadeias de caracteres literais. Se um sinal de aspas simples (') fizer parte da cadeia de caracteres literal, ele poderá ser representado por duas aspas simples (''). `SET QUOTED_IDENTIFIER` precisará ser ON quando palavras-chave reservadas forem usadas para nomes de objetos no banco de dados.

Quando `SET QUOTED_IDENTIFIER` for OFF, os identificadores não poderão estar entre aspas e precisarão seguir todas as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md). Literais podem ser delimitados por aspas simples ou duplas. Se uma cadeia de caracteres literal estiver delimitada por aspas duplas, a cadeia de caracteres poderá conter aspas simples inseridas, como apóstrofos.

> [!NOTE]
> QUOTED_IDENTIFIER não afeta os identificadores delimitados entre colchetes ([ ]).

`SET QUOTED_IDENTIFIER` precisará ser ON ao criar ou alterar índices em colunas computadas ou exibições indexadas. Se `SET QUOTED_IDENTIFIER` for OFF, as instruções CREATE, UPDATE, INSERT e DELETE falharão nas tabelas com índices em colunas computadas ou nas tabelas com exibições indexadas. Para obter mais informações sobre as configurações da opção SET necessárias com exibições indexadas e índices em colunas computadas, confira [Considerações sobre o uso das instruções SET](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements).

`SET QUOTED_IDENTIFIER` precisará ser ON quando você estiver criando um índice filtrado.

`SET QUOTED_IDENTIFIER` precisará ser ON quando você invocar métodos de tipo de dados XML.

O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem QUOTED_IDENTIFIER automaticamente como ON durante a conexão. Isso pode ser configurado em fontes de dados ODBC, em atributos de conexão ODBC ou em propriedades de conexão OLE DB. O padrão para SET QUOTED_IDENTIFIER é OFF para conexões de aplicativos DB-Library.

Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela mesmo que a opção esteja definida como OFF quando a tabela é criada.

Quando um procedimento armazenado é criado, as configurações SET QUOTED_IDENTIFIER e SET ANSI_NULLS são capturadas e usadas para invocações subsequentes desse procedimento armazenado.

Quando executada dentro de um procedimento armazenado, a configuração de SET QUOTED_IDENTIFIER não é alterada.

Quando `SET ANSI_DEFAULTS` for ON, o QUOTED_IDENTIFIER também será ON.

`SET QUOTED_IDENTIFIER` também corresponde à configuração QUOTED_IDENTIFIER de [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

`SET QUOTED_IDENTIFIER` entra em vigor no momento da análise [!INCLUDE[tsql](../../includes/tsql-md.md)] e afeta apenas a análise, não a otimização de consulta nem a execução da consulta.

Para um lote ad hoc de nível superior, a análise começa usando a configuração atual da sessão para QUOTED_IDENTIFIER. Conforme o lote for analisado, qualquer ocorrência de `SET QUOTED_IDENTIFIER` mudará o comportamento de análise desse ponto em diante e salvará essa configuração para a sessão. Portanto, depois que o lote for analisado e executado, a configuração QUOTED_IDENTIFER da sessão será definida de acordo com a última ocorrência de `SET QUOTED_IDENTIFIER` no lote.

O [!INCLUDE[tsql](../../includes/tsql-md.md)] estático em um procedimento armazenado é analisado usando a configuração QUOTED_IDENTIFIER em vigor para o lote que criou ou alterou o procedimento armazenado. `SET QUOTED_IDENTIFIER` não tem efeito quando aparece no corpo de um procedimento armazenado como [!INCLUDE[tsql](../../includes/tsql-md.md)] estático.

Para um lote aninhado que usa `sp_executesql` ou `exec()`, a análise é iniciada com a configuração QUOTED_IDENTIFIER da sessão. Se o lote aninhado estiver em um procedimento armazenado, a análise será iniciada com a configuração QUOTED_IDENTIFIER do procedimento armazenado. Conforme o lote aninhado for analisado, qualquer ocorrência de `SET QUOTED_IDENTIFIER` mudará o comportamento de análise desse ponto em diante, mas a configuração QUOTED_IDENTIFIER da sessão não será atualizada.

Para exibir a configuração atual dessa configuração, execute a seguinte consulta:

```sql
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';
IF ( (256 & @@OPTIONS) = 256 ) 
SET @QUOTED_IDENTIFIER = 'ON';

SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;
```

## <a name="permissions"></a>Permissões
Exige a associação à função `PUBLIC`.

## <a name="examples"></a>Exemplos

### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>a. Usando uma configuração de identificador entre aspas e nomes de objetos de palavra reservada

O exemplo a seguir mostra que a configuração de `SET QUOTED_IDENTIFIER` deve estar `ON`, e as palavras-chave em nomes de tabelas devem estar entre aspas duplas para criar e usar objetos que têm nomes de palavras-chave reservados.

```sql
SET QUOTED_IDENTIFIER OFF
GO

-- Create statement fails.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Create statement succeeds.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SELECT "identity","order"
FROM "select"
ORDER BY "order";
GO

DROP TABLE "SELECT";
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. Usando uma configuração de identificador entre aspas simples e duplas

 O exemplo a seguir mostra a maneira como aspas simples e duplas são usadas em expressões de cadeias de caracteres com `SET QUOTED_IDENTIFIER` dedinido como `ON` e `OFF`.

```sql
SET QUOTED_IDENTIFIER OFF;
GO

USE AdventureWorks2012;
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_NAME = 'Test')
    DROP TABLE dbo.Test;
GO
USE AdventureWorks2012;
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;
GO

-- Literal strings can be in single or double quotation marks.
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Strings inside double quotation marks are now treated
-- as object names, so they cannot be used for literals.
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');
GO

-- Object identifiers do not have to be in double quotation marks
-- if they are not reserved keywords.
SELECT ID, String
FROM dbo.Test;
GO

DROP TABLE dbo.Test;
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
 ID          String
 ----------- ------------------------------
 1           'Text in single quotes'
 2           'Text in single quotes'
 3           Text with 2 '' single quotes
 4           "Text in double quotes"
 5           "Text in double quotes"
 6           Text with 2 "" double quotes
 7           Text with a single ' quote
 ```

## <a name="see-also"></a>Consulte Também
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)    
[CREATE DEFAULT](../../t-sql/statements/create-default-transact-sql.md)    
[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)    
[CREATE RULE](../../t-sql/statements/create-rule-transact-sql.md)    
[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)    
[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)    
[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)    
[Tipos de dados](../../t-sql/data-types/data-types-transact-sql.md)    
[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)    
[SELECT](../../t-sql/queries/select-transact-sql.md)    
[Instruções SET](../../t-sql/statements/set-statements-transact-sql.md)    
[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)    
[sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)    
[Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md)
