---
description: CREATE ROLE (Transact-SQL)
title: CREATE ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0ca6f481b84cfd1453359e3b77d47bb5a6b52b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458766"
---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cria uma nova função de banco de dados no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *role_name*  
 É o nome da função a ser criada.  
  
 AUTHORIZATION *owner_name*  
 É o usuário de banco de dados ou função que terá a propriedade da nova função. Se nenhum usuário for especificado, a função será de propriedade do usuário que executar CREATE ROLE. O proprietário da função ou qualquer membro de uma função proprietária pode adicionar ou remover membros da função.
  
## <a name="remarks"></a>Comentários  
 As funções são protegíveis no nível de banco de dados. Depois de criar uma função, configure as permissões em nível de banco de dados da função usando GRANT, DENY e REVOKE. Para adicionar membros a uma função de banco de dados, use [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md). Para obter mais informações, veja [Funções em nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 As funções de banco de dados são visíveis nas exibições do catálogo sys.database_role_members e sys.database_principals.  
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **CREATE ROLE** no banco de dados, ou a associação na função de banco de dados fixa **db_securityadmin**. Ao usar a opção de **AUTHORIZATION**, as seguintes permissões também são necessárias:  
  
-   Para atribuir a propriedade de uma função a outro usuário, requer permissão IMPERSONATE naquele usuário.  
  
-   Para atribuir a propriedade de uma função para outra, requer associação na função de destinatário ou a permissão ALTER nessa função.  
  
-   Para atribuir a propriedade de uma função a uma função de aplicativo é necessária a permissão ALTER na função de aplicativo.  
  
## <a name="examples"></a>Exemplos  
Os seguintes exemplos usam todos o banco de dados AdventureWorks.   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>a. Criando uma função de banco de dados pertencente a um usuário de banco de dados  
 O exemplo a seguir cria a função de banco de dados `buyers` que pertence ao usuário `BenMiller`.  
  
```sql  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. Criando uma função de banco de dados pertencente a uma função de banco de dados fixa  
 O exemplo a seguir cria a função de banco de dados `auditors` que é de propriedade da função de banco de dados fixa `db_securityadmin`.  
  
```sql  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


