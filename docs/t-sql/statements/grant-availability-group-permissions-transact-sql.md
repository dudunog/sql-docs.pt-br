---
title: Permissões de grupo de disponibilidade GRANT
description: Concede permissões em um Grupo de Disponibilidade Always On.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7c25b8f0395694bdb85cddbb5ec1bf0abf86c9d4
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86483585"
---
# <a name="grant-availability-group-permissions-transact-sql"></a>Permissões de grupo de disponibilidade GRANT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Concede permissões em um Grupo de Disponibilidade AlwaysOn.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *permission*  
 Especifica uma permissão que pode ser concedida em um grupo de disponibilidade. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ON AVAILABILITY GROUP **::** _availability_group_name_  
 Especifica o grupo de disponibilidade no qual a permissão está sendo concedida. O qualificador de escopo ( **::** ) é obrigatório.  
  
 TO \<server_principal>  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual a permissão está sendo concedida.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do qual o principal que executa esta consulta deriva seu direito de conceder a permissão.  
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo de servidor podem ser concedidas somente quando o banco de dados atual for **mestre**.  
  
 Informações sobre grupos de disponibilidade são visíveis na exibição do catálogo [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md). As informações sobre permissões de servidor estão visíveis na exibição do catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) e as informações sobre entidades de segurança do servidor estão visíveis na exibição do catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Um grupo de disponibilidade é um nível de servidor protegível. As permissões mais específicas e limitadas que podem ser concedidas em um grupo de disponibilidade são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de grupo de disponibilidade|Implícito na permissão de grupo de disponibilidade|Implícito na permissão de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONECTAR|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 Para um gráfico de todas as permissões [!INCLUDE[ssDE](../../includes/ssde-md.md)], veja [Pôster de permissão do mecanismo de banco de dados](https://aka.ms/sql-permissions-poster).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no grupo de disponibilidade ou a permissão ALTER ANY AVAILABILITY GROUP no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>a. Concedendo a permissão VIEW DEFINITION em um grupo de disponibilidade  
 O exemplo a seguir concede a permissão `VIEW DEFINITION` no grupo de disponibilidade `MyAg` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon `ZArifin`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. Concedendo a permissão TAKE OWNERSHIP com GRANT OPTION  
 O exemplo a seguir concede a permissão `TAKE OWNERSHIP` no grupo de disponibilidade `MyAg` para o usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`PKomosinski` com `GRANT OPTION`.  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. Concedendo a permissão CONTROL em um grupo de disponibilidade  
 O exemplo a seguir concede a permissão `CONTROL` no grupo de disponibilidade `MyAg` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário `PKomosinski`. CONTROL permite o controle completo de logon do grupo de disponibilidade, embora eles não sejam o proprietário do grupo de disponibilidade. Para alterar a propriedade, veja [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões REVOKE do grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [Permissões DENY de grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Exibições do catálogo de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [Permissões &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
