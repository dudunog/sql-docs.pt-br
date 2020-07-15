---
title: ALTER APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_APPLICATION_ROLE_TSQL
- ALTER APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying application roles
- passwords [SQL Server], application roles
- ALTER APPLICATION ROLE statement
- application roles [SQL Server], modifying
ms.assetid: c6cd5d0f-18f4-49be-b161-64d9c5569086
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6b0d65b5d4d68ac23f980e98405d4c19e0e970e1
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86302015"
---
# <a name="alter-application-role-transact-sql"></a>ALTER APPLICATION ROLE (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Altera o nome, a senha ou o esquema padrão de uma função de aplicativo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe
  
```syntaxsql
  
ALTER APPLICATION ROLE application_role_name
    WITH <set_item> [ ,...n ]  
  
<set_item> ::=
    NAME = new_application_role_name
    | PASSWORD = 'password'  
    | DEFAULT_SCHEMA = schema_name  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

 *application_role_name*  
 É o nome da função de aplicativo a ser modificada.  
  
 NAME =*new_application_role_name*  
 Especifica o novo nome da função de aplicativo. Esse nome ainda não deve ser usado para referenciar qualquer entidade no banco de dados.  
  
 PASSWORD ='*password*'  
 Especifica a senha da função de aplicativo. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você sempre deve usar senhas fortes.  
  
 DEFAULT_SCHEMA =*schema_name*  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos. *schema_name* pode ser um esquema que não existe no banco de dados.  
  
## <a name="remarks"></a>Comentários

Se o novo nome da função de aplicativo já existir no banco de dados, a instrução falhará. Quando o nome, a senha ou o esquema padrão de uma função de aplicativo é alterado, a ID associada à função não é alterada.  
  
> [!IMPORTANT]  
>  A política de expiração de senha não é aplicada às senhas de função de aplicativo. Por esse motivo, tome muito cuidado ao selecionar senhas fortes. Os aplicativos que invocam funções de aplicativo devem armazenar suas senhas.  
  
 As funções de aplicativo são visíveis na exibição do catálogo sys.database_principals.  
  
> [!CAUTION]  
>  No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o comportamento de esquemas mudou em relação ao comportamento em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código que pressupõe que esquemas são equivalentes a usuários de banco de dados pode não retornar resultados corretos. Exibições de catálogo antigas, incluindo sysobjects, não devem ser usadas em um banco de dados no qual uma das instruções DDL a seguir já tenha sido utilizada: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. Em um banco de dados no qual qualquer uma dessas instruções tenha sido usada alguma vez, você deve usar as novas exibições do catálogo. As novas exibições do catálogo levam em conta a separação de entidades e esquemas introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para mais informações sobre exibições do catálogo, consulte [Exibições do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados. Para alterar o esquema padrão, o usuário também precisa da permissão ALTER na função de aplicativo. Uma função de aplicativo pode alterar seu próprio esquema padrão, mas não seu nome ou senha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-name-of-application-role"></a>a. Alterando o nome da função de aplicativo  
 O exemplo a seguir altera o nome da função de aplicativo `weekly_receipts` para `receipts_ledger`.  
  
```sql  
USE AdventureWorks2012;  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987Gbv8$76sPYY5m23' ,   
    DEFAULT_SCHEMA = Sales;  
GO  
ALTER APPLICATION ROLE weekly_receipts   
    WITH NAME = receipts_ledger;  
GO  
```  
  
### <a name="b-changing-the-password-of-application-role"></a>B. Alterando a senha da função de aplicativo  
 O exemplo a seguir altera a senha da função de aplicativo `receipts_ledger`.  
  
```sql  
ALTER APPLICATION ROLE receipts_ledger   
    WITH PASSWORD = '897yUUbv867y$200nk2i';  
GO  
```  
  
### <a name="c-changing-the-name-password-and-default-schema"></a>C. Alterando o nome, a senha e o esquema padrão  
 O exemplo a seguir altera o nome, a senha e o esquema padrão da função de aplicativo `receipts_ledger` ao mesmo tempo.  
  
```sql  
ALTER APPLICATION ROLE receipts_ledger   
    WITH NAME = weekly_ledger,   
    PASSWORD = '897yUUbv77bsrEE00nk2i',   
    DEFAULT_SCHEMA = Production;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de Aplicativo](../../relational-databases/security/authentication-access/application-roles.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
