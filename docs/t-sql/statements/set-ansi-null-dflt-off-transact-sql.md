---
description: SET ANSI_NULL_DFLT_OFF (Transact-SQL)
title: SET ANSI_NULL_DFLT_OFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ANSI_NULL_DFLT_OFF_TSQL
- ANSI_NULL_DFLT_OFF
- SET ANSI_NULL_DFLT_OFF
- SET_ANSI_NULL_DFLT_OFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- default nullability
- ANSI_NULL_DFLT_OFF option
- null values [SQL Server], overriding
- overriding default nullability
- SET ANSI_NULL_DFLT_OFF statement
ms.assetid: 8ed5c512-f5de-4741-a18a-de85a3041295
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0141e6a854da807287fc1ab9b12fc8599489a9e1
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98080506"
---
# <a name="set-ansi_null_dflt_off-transact-sql"></a>SET ANSI_NULL_DFLT_OFF (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Altera o comportamento da sessão para substituir a possibilidade de nulidade padrão de novas colunas quando a opção padrão nula ANSI do banco de dados é **true**. Para obter mais informações sobre como configurar o valor para padrão nulo ANSI, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database
  
SET ANSI_NULL_DFLT_OFF { ON | OFF }
```

```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse

SET ANSI_NULL_DFLT_OFF OFF
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
 Esta configuração somente afetará a capacidade de nulidade de novas colunas quando a capacidade de nulidade da coluna não estiver especificada nas instruções CREATE TABLE e ALTER TABLE. Por padrão, quando SET ANSI_NULL_DFLT_OFF for ON, novas colunas criadas com o uso das instruções ALTER TABLE e CREATE TABLE serão NOT NULL se o status da capacidade de nulidade da coluna não for especificado explicitamente. SET ANSI_NULL_DFLT_OFF não afeta as colunas criadas com o uso de um NULL ou NOT NULL explícito.  
  
 SET ANSI_NULL_DFLT_OFF e SET ANSI_NULL_DFLT_ON não podem ser definidos como ON ao mesmo tempo. Se uma opção for definida como ON, a outra será definida como OFF. Portanto, ANSI_NULL_DFLT_OFF ou SET ANSI_NULL_DFLT_ON pode ser definido como ON ou ambos podem ser definidos como OFF. Se uma das opções for ON, essa configuração (SET ANSI_NULL_DFLT_OFF ou SET ANSI_NULL_DFLT_ON) entrará em vigor. Se ambas as opções forem definidas como OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o valor da coluna is_ansi_null_default_on na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 Para uma operação mais confiável dos scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] usados em bancos de dados com diferentes configurações de capacidade de nulidade, é melhor sempre especificar NULL ou NOT NULL nas instruções CREATE TABLE e ALTER TABLE.  
  
 A configuração de SET ANSI_NULL_DFLT_OFF é definida no momento da execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```sql  
DECLARE @ANSI_NULL_DFLT_OFF VARCHAR(3) = 'OFF';  
IF ( (2048 & @@OPTIONS) = 2048 ) SET @ANSI_NULL_DFLT_OFF = 'ON';  
SELECT @ANSI_NULL_DFLT_OFF AS ANSI_NULL_DFLT_OFF;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra os efeitos de `SET ANSI_NULL_DFLT_OFF` com ambas as configurações da opção de banco de dados Padrão ANSI null.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
-- Set the 'ANSI null default' database option to true by executing   
-- ALTER DATABASE.  
GO  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON;  
GO  
-- Create table t1.  
CREATE TABLE t1 (a TINYINT);  
GO  
-- NULL INSERT should succeed.  
INSERT INTO t1 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to ON and create table t2.  
SET ANSI_NULL_DFLT_OFF ON;  
GO  
CREATE TABLE t2 (a TINYINT);  
GO   
-- NULL INSERT should fail.  
INSERT INTO t2 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to OFF and create table t3.  
SET ANSI_NULL_DFLT_OFF OFF;  
GO  
CREATE TABLE t3 (a TINYINT) ;  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t3 (a) VALUES (NULL);  
GO  
  
-- This illustrates the effect of having both the database  
-- option and SET option disabled.  
-- Set the 'ANSI null default' database option to false.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT OFF;  
GO  
-- Create table t4.  
CREATE TABLE t4 (a TINYINT) ;  
GO   
-- NULL INSERT should fail.  
INSERT INTO t4 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to ON and create table t5.  
SET ANSI_NULL_DFLT_OFF ON;  
GO  
CREATE TABLE t5 (a TINYINT);  
GO   
-- NULL insert should fail.  
INSERT INTO t5 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to OFF and create table t6.  
SET ANSI_NULL_DFLT_OFF OFF;  
GO  
CREATE TABLE t6 (a TINYINT);   
GO   
-- NULL insert should fail.  
INSERT INTO t6 (a) VALUES (NULL);  
GO  
  
-- Drop tables t1 through t6.  
DROP TABLE t1, t2, t3, t4, t5, t6;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)  
  
  
