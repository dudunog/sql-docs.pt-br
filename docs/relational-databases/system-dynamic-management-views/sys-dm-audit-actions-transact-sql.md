---
title: sys. dm_audit_actions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e6a6c91cb31c9c3036bc95239f0aff9c75fda7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67936973"
---
# <a name="sysdm_audit_actions-transact-sql"></a>sys.dm_audit_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Retorna uma linha para cada ação de auditoria que pode ser reportada no log de auditoria e para cada grupo de ação de auditoria que pode ser configurado como parte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre auditoria, consulte [SQL Server audit &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar(4)**|ID da ação de auditoria. Relacionado ao valor de **action_id** gravados em cada registro de auditoria. Permite valor nulo. É NULL para grupos de auditoria.|  
|**action_in_log**|**bit**|Indica se uma ação pode ser gravada em um log de auditoria. Os valores são:<br /><br /> 1 = Sim<br /><br /> 0 = Não|  
|**name**|**sysname**|Nome da ação de auditoria ou do grupo de ações de auditoria. Não permite valor nulo.|  
|**class_desc**|**nvarchar(120)**|O nome da classe do objeto ao qual a ação de auditoria aplica-se. Pode ser qualquer objeto do escopo Servidor, Banco de dados ou Esquema, mas não inclui objetos Esquema. Não permite valor nulo.|  
|**parent_class_desc**|**nvarchar(120)**|Nome da classe pai do objeto descrito por class_desc. Será NULL se class_desc for Servidor.|  
|**covering_parent_action_name**|**nvarchar(120)**|Nome da ação de auditoria ou do grupo de auditoria que contém a ação de auditoria descrita nesta linha. É usada para criar uma hierarquia de ações e ações abrangentes. Permite valor nulo.|  
|**configuration_level**|**nvarchar (10)**|Indica que a ação ou o grupo de ações especificado nessa linha são configuráveis no nível do Grupo ou da Ação. Será NULL se a ação não for configurável.|  
|**containing_group_name**|**nvarchar(120)**|O nome do grupo de auditoria que contém a ação especificada. Será NULL se o valor em name for um grupo.|  
  
## <a name="permissions"></a>Permissões  
 As entidades de segurança devem ter a permissão **Select** . Por padrão, é concedida a Público.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)].  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR auditoria de servidor &#40;&#41;Transact-SQL](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [Descartar auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CRIAR especificação de auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de alteração de auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria DROP SERVER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CRIAR especificação de auditoria de banco de dados &#40;&#41;Transact-SQL](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys. fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys. server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys. server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys. server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys. server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys. database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys. database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys. dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys. dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
