---
description: DROP DATABASE SCOPED CREDENTIAL (Transact-SQL)
title: DROP DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a4ac1f679400a021b8a61b0e5c0b3adbdffcdf29
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380081"
---
# <a name="drop-database-scoped-credential-transact-sql"></a>DROP DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

  Remove uma credencial no escopo do banco de dados do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 É o nome da credencial no escopo do banco de dados a ser removida do servidor.  
  
## <a name="remarks"></a>Comentários  
 Para remover o segredo associado a uma credencial no escopo do banco de dados sem remover a credencial propriamente dita, use [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Informações sobre credenciais no escopo do banco de dados ficam visíveis na exibição do catálogo [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER` na credencial.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a credencial no escopo do banco de dados chamada `SalesAccess`.  
  
```sql  
DROP DATABASE SCOPED CREDENTIAL SalesAccess;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
