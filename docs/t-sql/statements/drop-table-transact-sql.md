---
description: DROP TABLE (Transact-SQL)
title: DROP TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_TABLE_TSQL
- DROP TABLE
dev_langs:
- TSQL
helpviewer_keywords:
- removing indexes
- table removal [SQL Server]
- deleting indexes
- dropping data
- deleting tables
- dropping indexes
- removing constraints
- removing permissions
- DROP TABLE statement
- removing tables
- deleting triggers
- removing data
- dropping tables
- deleting permissions
- dropping triggers
- deleting constraints
- removing triggers
- deleting data
- dropping constraints
- dropping permissions
ms.assetid: 0b6f2b6f-3aa3-4767-943f-43df3c3c5cfd
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 246ba275b1e918f063e05b22d9ec3637b9a5631e
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099418"
---
# <a name="drop-table-transact-sql"></a>DROP TABLE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove uma ou mais definições de tabela e todos os dados, índices, gatilhos, restrições e especificações de permissão dessas tabelas. Qualquer exibição ou procedimento armazenado que faça referência à tabela descartada deverá ser descartado explicitamente utilizando [DROP VIEW](../../t-sql/statements/drop-view-transact-sql.md) ou [DROP PROCEDURE](../../t-sql/statements/drop-procedure-transact-sql.md). Para relatar as dependências em uma tabela, use [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
DROP TABLE [ IF EXISTS ] { database_name.schema_name.table_name | schema_name.table_name | table_name } [ ,...n ]  
[ ; ]  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
DROP TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name*  
 É o nome do banco de dados no qual a tabela foi criada.  
  
 O Banco de Dados SQL do Azure oferece suporte ao formato de nome de três partes database_name.[schema_name].object_name quando o database_name é o banco de dados atual ou o database_name é tempdb e o object_name começa com #. O Banco de Dados SQL do Azure não oferece suporte a nomes de quatro partes.  
  
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente a tabela somente se ela já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome da tabela a ser removida.  
  
## <a name="remarks"></a>Comentários  
 DROP TABLE não pode ser usado para descartar uma tabela que é referenciada por uma restrição FOREIGN KEY. A restrição FOREIGN KEY que faz referência ou a tabela de referência deve ser primeiramente descartada. Se a tabela de referência e a tabela que contém a chave primária forem descartadas na mesma instrução DROP TABLE, a tabela de referência deverá ser listada em primeiro lugar.  
  
 Podem ser descartadas várias tabelas em qualquer banco de dados. Se uma tabela que está sendo descartada fizer referência à chave primária de outra tabela que também está sendo descartada, a tabela de referência com a chave estrangeira deverá ser listada antes da tabela que contém a chave primária que está sendo referenciada.  
  
 Quando uma tabela for descartada, as regras ou os padrões da tabela perderão sua associação e quaisquer restrições ou gatilhos associados à tabela serão descartados automaticamente. Se você recriar uma tabela, deverá associar novamente as regras e padrões apropriados, recriar quaisquer gatilhos e adicionar todas as restrições necessárias.  
  
 Se você excluir todas as linhas de uma tabela usando DELETE *tablename* ou usar a instrução TRUNCATE TABLE, a tabela existirá até que ela seja descartada.  
  
 Tabelas e índices grandes que usem mais de 128 extensões são descartados em duas fases separadas: a fase lógica e a física. Na fase lógica, as unidades de alocação existentes usadas pela tabela são marcadas para desalocação e bloqueadas até que a transação seja confirmada. Na fase física, as páginas IAM marcadas para desalocação são descartadas fisicamente em lotes.  
  
 Se você descartar uma tabela que contém uma coluna VARBINARY(MAX) com o atributo FILESTREAM, os dados armazenados no sistema de arquivos não serão removidos.  
  
> [!IMPORTANT]  
>  DROP TABLE e CREATE TABLE não devem ser executados na mesma tabela no mesmo lote. Caso contrário, poderá ocorrer um erro inesperado.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão ALTER no esquema ao qual a tabela pertence, permissão CONTROL na tabela ou associação na função de banco de dados fixa **db_ddladmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-table-in-the-current-database"></a>a. Descartando uma tabela no banco de dados atual  
 O exemplo a seguir remove a tabela `ProductVendor1` e seus dados e índices do banco de dados atual.  
  
```sql  
DROP TABLE ProductVendor1 ;  
```  
  
### <a name="b-dropping-a-table-in-another-database"></a>B. Descartando uma tabela em outro banco de dados  
 O exemplo a seguir descarta a tabela `SalesPerson2` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. O exemplo pode ser executado a partir de qualquer banco de dados na instância do servidor.  
  
```sql  
DROP TABLE AdventureWorks2012.dbo.SalesPerson2 ;  
```  
  
### <a name="c-dropping-a-temporary-table"></a>C. Descartando uma tabela temporária  
 O exemplo a seguir cria uma tabela temporária, testa sua existência, descarta a mesma e testa novamente sua existência. Este exemplo não usa a sintaxe **IF EXISTS** que está disponível com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```sql  
CREATE TABLE #temptable (col1 INT);  
GO  
INSERT INTO #temptable  
VALUES (10);  
GO  
SELECT * FROM #temptable;  
GO  
IF OBJECT_ID(N'tempdb..#temptable', N'U') IS NOT NULL   
DROP TABLE #temptable;  
GO  
--Test the drop.  
SELECT * FROM #temptable;  
```  
  
### <a name="d-dropping-a-table-using-if-exists"></a>D. Descartando uma tabela usando IF EXISTS  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 O exemplo a seguir cria uma tabela chamada T1. Em seguida, a segunda instrução remove a tabela. A terceira instrução não realiza nenhuma ação porque a tabela já foi excluída, porém, não causa um erro.  
  
```sql  
CREATE TABLE T1 (Col1 INT);  
GO  
DROP TABLE IF EXISTS T1;  
GO  
DROP TABLE IF EXISTS T1;  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
