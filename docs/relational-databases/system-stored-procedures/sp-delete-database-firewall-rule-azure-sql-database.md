---
description: sp_delete_database_firewall_rule (Banco de Dados SQL do Azure)
title: sp_delete_database_firewall_rule (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_database_firewall_rule
- sp_delete_database_firewall_rule_TSQL
- sys.sp_delete_database_firewall_rule
- sys.sp_delete_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_database_firewall_rule procedure
ms.assetid: ed295312-e586-4fc2-9e80-806b490ee7bd
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current
ms.openlocfilehash: ae71838bd9a384e616d0f1fe50d612535f840919
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472687"
---
# <a name="sp_delete_database_firewall_rule-azure-sql-database"></a>sp_delete_database_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  Remove a configuração de firewall no nível de banco de dados do seu [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] . As regras de firewall de banco de dados podem ser configuradas e excluídas para o banco de dados mestre e para bancos de dados de usuário no [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] .   
  
 
## <a name="syntax"></a>Sintaxe  
  
```    
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 `[@name =] [N]'name'`  
 O nome da configuração de firewall de nível de banco de dados que será removida. *nome* é **nvarchar (128)** sem valor padrão. O identificador Unicode `N` é opcional para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] . 
  
## <a name="permissions"></a>Permissões  
 Somente o logon da entidade de segurança no nível do servidor criado pelo processo de provisionamento ou uma entidade de Azure Active Directory atribuída como administrador pode excluir regras de firewall no nível de banco de dados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir remove a configuração de firewall no nível de banco de dados chamada `Example DB Setting 1` .
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Firewall do banco de dados SQL do Azure](/azure/azure-sql/database/firewall-configure)   
 [Como: definir configurações de firewall (banco de dados SQL do Azure)](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
