---
title: DROP PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ed342f6b73ee596d8429aa4b952c4becf7d41ab
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68044033"
---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove um ou mais procedimentos armazenados ou grupos de procedimentos do banco de dados atual no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente o procedimento somente se ele já existe.  
  
 *schema_name*  
 O nome do esquema ao qual o procedimento pertence. Não é possível especificar um nome de servidor ou de banco de dados.  
  
 *procedure*  
 O nome do procedimento armazenado ou grupo de procedimentos armazenados a ser removido. Não é possível descartar procedimentos individuais em um grupo de procedimentos numerados; todo o grupo de procedimentos é descartado.  
  
## <a name="best-practices"></a>Práticas Recomendadas  
 Antes de remover qualquer procedimento armazenado, verifique se há objetos dependentes e modifique esses objetos adequadamente. Descartar um procedimento armazenado pode gerar falha de objetos e scripts dependentes quando esses objetos não forem atualizados. Para obter mais informações, veja [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>Metadados  
 Para exibir uma lista de procedimentos existentes, veja a exibição de catálogo **sys.objects**. Para exibir a definição do procedimento, veja a exibição do catálogo **sys.sql_modules**.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão **CONTROL** no procedimento, ou a permissão **ALTER** no esquema ao qual o procedimento pertence ou a associação na função de servidor fixa **db_ddladmin**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o procedimento armazenado `dbo.uspMyProc` do banco de dados atual.  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 O exemplo a seguir remove vários procedimentos armazenados do banco de dados atual.  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 O exemplo a seguir remove o procedimento armazenado `dbo.uspMyProc` se ele existe, mas não causa um erro se o procedimento não existe. Essa sintaxe é nova no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Excluir um procedimento armazenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  


