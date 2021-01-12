---
description: USE (Transact-SQL)
title: USE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs:
- TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
author: cawrites
ms.author: chadam
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f31381a2c43d02af5b3c19478fcf03e7bcc608d6
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095882"
---
# <a name="use-transact-sql"></a>USE (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  Altera o contexto de banco de dados para o banco de dados ou instantâneo de banco de dados especificado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
USE { database_name }   
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name*  
 É o nome do banco de dados ou instantâneo de banco de dados para os quais o contexto de usuário é alternado. Os nomes do banco de dados e do instantâneo do banco de dados devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 Em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o parâmetro de banco de dados só pode se referir ao banco de dados atual. Se um banco de dados que não seja o banco de dados atual é fornecido, a instrução `USE` não alterna entre bancos de dados e o código de erro 40508 é retornado. Para alterar os bancos de dados, você deve conectar-se diretamente ao banco de dados. A instrução USE é marcada como não aplicável ao Banco de Dados SQL na parte superior desta página, porque, embora você possa ter a instrução `USE` em um lote, ela não executa nenhuma ação.
  
## <a name="remarks"></a>Comentários  
 Quando um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele é automaticamente conectado ao seu banco de dados padrão e adquire o contexto de segurança de um usuário de banco de dados. Se nenhum usuário de banco de dados foi criado para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o logon se conectará como convidado. Se o usuário de banco de dados não tiver permissão CONNECT no banco de dados, a instrução USE falhará. Se nenhum banco de dados padrão foi atribuído ao logon, seu banco de dados padrão será definido como mestre.  
  
 USE é executado em tempo de compilação e de execução e entra em vigor imediatamente. Portanto, as instruções exibidas em um lote depois da instrução USE são executadas no banco de dados especificado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão de CONNECT no banco de dados de destino.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o contexto de banco de dados para o banco de dados `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../statements/create-database-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
