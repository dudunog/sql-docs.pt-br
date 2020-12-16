---
description: ALTER SERVER ROLE (Transact-SQL)
title: ALTER SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f9c922af5cb3dcca795cb095aebea4875c9f18c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483938"
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

Altera a associação de uma função de servidor ou altera nome de uma função de servidor definida pelo usuário. As funções de servidor fixas não podem ser renomeadas.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>Argumentos  
*server_role_name*  
É o nome da função de servidor a ser alterada.  
  
ADD MEMBER *server_principal*  
Adiciona a entidade de segurança do servidor especificado à função de servidor. *server_principal* pode ser um logon ou uma função de servidor definida pelo usuário. *server_principal* não pode ser uma função de servidor fixa, uma função de banco de dados nem sa.  
  
DROP MEMBER *server_principal*  
Remove a entidade de segurança de servidor especificada da função de servidor. *server_principal* pode ser um logon ou uma função de servidor definida pelo usuário. *server_principal* não pode ser uma função de servidor fixa, uma função de banco de dados nem sa.  
  
WITH NAME **=** _new_server_role_name_  
Especifica o novo nome da função de servidor definida pelo usuário. Esse nome ainda não pode existir no servidor.  
  
## <a name="remarks"></a>Comentários  
A alteração do nome de uma função de servidor definida pelo usuário não altera o número da ID, o proprietário ou as permissões da função.  
  
Para alterar a associação de função, `ALTER SERVER ROLE` substitui sp_addsrvrolemember e sp_dropsrvrolemember. Esses procedimentos armazenados foram preteridos.  
  
É possível exibir as funções de servidor por meio de consulta das exibições do catálogo `sys.server_role_members` e `sys.server_principals`.  
  
Para alterar o proprietário de uma função de servidor definida pelo usuário, use [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
Requer a permissão `ALTER ANY SERVER ROLE` no servidor para alterar o nome de uma função de servidor definida pelo usuário.  
  
**Funções fixas de servidor**  
  
Para adicionar um membro a uma função de servidor fixa, você deve ser membro dessa função de servidor fixa ou da função de servidor fixa `sysadmin`.  
  
> [!NOTE]  
>  As permissões `CONTROL SERVER` e `ALTER ANY SERVER ROLE` não são suficientes para executar `ALTER SERVER ROLE` para uma função de servidor fixa, e a `ALTER` permissão não pode ser concedida em uma função de servidor fixa.  
  
**Funções de servidor definidas pelo usuário**  
  
Para adicionar um membro a uma função de servidor definida pelo usuário, você deve ser um membro da função fixa de servidor `sysadmin` ou ter a permissão `CONTROL SERVER` ou `ALTER ANY SERVER ROLE`. Ou você deve ter a permissão `ALTER` naquela função.  
  
> [!NOTE]  
>  Ao contrário das funções de servidor fixas, os membros de uma função de servidor definida pelo usuário não têm permissão inerentemente para adicionar membros àquela mesma função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-name-of-a-server-role"></a>a. Alterando o nome de uma função de servidor  
O exemplo seguinte cria uma função de servidor chamada `Product` e, em seguida, altera o nome da função de servidor para `Production`.  
  
```sql
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. Adicionando uma conta de domínio a uma função de servidor.  
O exemplo a seguir adiciona uma conta de domínio chamada `adventure-works\roberto0` à função de servidor definida pelo usuário chamada `Production`.  
  
```sql
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. Adicionando um logon do SQL Server a uma função de servidor  
O exemplo a seguir adiciona o logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamado `Ted` à função fixa de servidor `diskadmin`.  
  
```sql
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. Removendo uma conta de domínio de uma função de servidor  
O exemplo a seguir remove uma conta de domínio chamada `adventure-works\roberto0` da função de servidor definida pelo usuário chamada `Production`.  
  
```sql
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. Removendo um logon do SQL Server de uma função de servidor  
O exemplo a seguir remove o logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Ted` da função fixa de servidor `diskadmin`.  
  
```sql
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. Concedendo a um logon a permissão para adicionar logons a uma função de servidor definida pelo usuário  
O exemplo a seguir permite que `Ted` adicione outros logons à função de servidor definida pelo usuário chamada `Production`.  
  
```sql
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. Para exibir a associação de função  
Para exibir a associação de função, use a página **Função de Servidor (Membros)** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou execute a seguinte consulta:  
  
```sql
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. Sintaxe básica  
O exemplo a seguir adiciona o logon no `Anna` à função de servidor `LargeRC`.  
  
```sql
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. Remova um logon de uma classe de recurso.  
O exemplo a seguir remove a associação de Ana na função de servidor `LargeRC`.  
  
```sql
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>Consulte Também  
[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
