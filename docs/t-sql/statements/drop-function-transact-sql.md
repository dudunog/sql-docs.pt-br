---
description: DROP FUNCTION (Transact-SQL)
title: DROP FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 655cf93adfd1fbc84d6ab6333fb42e88a66826dd
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096932"
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove uma ou mais funções definidas pelo usuário do banco de dados atual. As funções definidas pelo usuário são criadas com [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) e modificadas com [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md).  
  
 A função DROP dá suporte a funções escalares definidas pelo usuário compiladas nativamente. Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```syntaxsql
 -- Azure Synapse Analytics, Parallel Data Warehouse 

DROP FUNCTION [IF EXISTS] [ schema_name. ] function_name
[;] 
```  
   
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *IF EXISTS*    
 Remove condicionalmente a função somente se ela já existe. Disponível do [!INCLUDE[ssnoversion_md](../../includes/ssnoversion-md.md)] 2016 e no [!INCLUDE[sssds_md](../../includes/sssds-md.md)].
  
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *function_name*  
 É o nome da função ou funções definidas pelo usuário a serem removidas. A especificação do nome de esquema é opcional. Não é possível especificar o nome de servidor e de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 DROP FUNCTION falhará se houver funções ou exibições [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados que referenciem essa função e forem criadas usando SCHEMABINDING, ou se houver colunas computadas, restrições CHECK ou DEFAULT que referenciem a função.  
  
 DROP FUNCTION falhará se houver colunas computadas que referenciem essa função e tenham sido indexadas.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP FUNCTION, no mínimo, um usuário deve ter permissão ALTER no esquema ao qual pertence a função definida pelo usuário ou permissão CONTROL na função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-function"></a>a. Descartando uma função  
 O exemplo a seguir remove a função definida pelo usuário `fn_SalesByStore` do esquema `Sales` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Para criar essa função, veja o exemplo B em [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
```sql  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
