---
title: sys. server_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: stevestein
ms.author: sstein
ms.openlocfilehash: 254be7cdd5e26422a27262b963d48908777d616b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133016"
---
# <a name="sysserver_sql_modules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém o conjunto de módulos SQL para gatilhos do nível do servidor de tipo TR. Você pode associar essa relação a sys.server_triggers. A tupla (object_id) é a chave da relação.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Esta é uma referência FOREIGN KEY ao gatilho no nível do servidor onde o módulo foi definido.|  
|**defini**|**nvarchar(max)**|Texto SQL que define esse módulo.<br /><br /> NULL = Criptografado.|  
|**uses_ansi_nulls**|**bit**|O módulo foi criado com a opção SET ANSI NULLS definida como ON.|  
|**uses_quoted_identifier**|**bit**|O módulo foi criado com a opção SET QUOTED IDENTIFIER definida como ON.|  
|**execute_as_principal_id**|**int**|A identificação do servidor principal EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER<br /><br /> ID da entidade de segurança especificada se EXECUTE AS SELF EXECUTE como principal-2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
