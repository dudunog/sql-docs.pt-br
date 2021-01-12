---
description: DROP DEFAULT (Transact-SQL)
title: DROP DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 43c75b4462f8a725e5ce06d4d5eb545000bc8bb7
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095752"
---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove um ou mais padrões definidos pelo usuário do banco de dados atual.  
  
> [!IMPORTANT]
>  DROP DEFAULT será removido na próxima versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use DROP DEFAULT em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente a utilizam. Em vez disso, use as definições padrão que você pode criar com a palavra-chave DEFAULT de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente o padrão somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual o padrão pertence.  
  
 *default_name*  
 É o nome de um padrão existente. Para ver uma lista dos padrões existentes, execute **sp_help**. Os padrões devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar o nome do esquema padrão é opcional.  
  
## <a name="remarks"></a>Comentários  
 Antes de remover um padrão, desassocie-o executando **sp_unbindefault** se ele estiver atualmente associado a uma coluna ou a um tipo de dados de alias.  
  
 Depois que um padrão é descartado de uma coluna que permite valores nulos, NULL é inserido nessa posição quando as linhas são adicionadas e nenhum valor é explicitamente fornecido. Depois que um padrão é descartado de uma coluna NOT NULL, uma mensagem de erro é retornada quando as linhas são adicionadas e nenhum valor é explicitamente fornecido. Estas linhas são adicionadas posteriormente como parte do comportamento da instrução INSERT típica.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP DEFAULT, no mínimo, um usuário deve ter a permissão ALTER no esquema ao qual o padrão pertence.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-default"></a>a. Descartando um padrão  
 Se um padrão não estiver associado a uma coluna ou a um tipo de dados de alias, ele só poderá ser descartado usando DROP DEFAULT. O exemplo a seguir remove o padrão criado pelo usuário chamado `datedflt`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode usar a sintaxe a seguir.  
  
```sql  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. Descartando um padrão associado a uma coluna  
 O exemplo a seguir desassocia o padrão associado à coluna `EmergencyContactPhone` da tabela `Contact` e descarta o padrão chamado `phonedflt`.  
  
```sql  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
