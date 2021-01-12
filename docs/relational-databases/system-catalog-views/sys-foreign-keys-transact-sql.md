---
description: sys.foreign_keys (Transact-SQL)
title: sys.foreign_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba0494d8ca1532f02e5f0cde92eef18d9a7d0639
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098020"
---
# <a name="sysforeign_keys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha por objeto que é uma restrição FOREIGN KEY, com **Sys. Object. Type** = F.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**referenced_object_id**|**int**|ID do objeto referenciado.|  
|**key_index_id**|**int**|ID do índice de chave no objeto referenciado.|  
|**is_disabled**|**bit**|A restrição FOREIGN KEY foi desabilitada.|  
|**is_not_for_replication**|**bit**|A restrição FOREIGN KEY foi criada com o uso da opção NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|A restrição FOREIGN KEY não foi verificada pelo sistema.|  
|**delete_referential_action**|**tinyint**|A ação referencial declarada para esse FOREIGN KEY quando ocorre uma exclusão.<br /><br /> 0 = Nenhuma ação<br /><br /> 1 = Cascata<br /><br /> 2 = Definido como nulo<br /><br /> 3 = Definir como padrão|  
|**delete_referential_action_desc**|**nvarchar(60)**|Descrição da ação referencial declarada para esse FOREIGN KEY quando ocorre uma exclusão:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|A ação referencial declarada para esse FOREIGN KEY quando ocorre uma atualização.<br /><br /> 0 = Nenhuma ação<br /><br /> 1 = Cascata<br /><br /> 2 = Definido como nulo<br /><br /> 3 = Definir como padrão|  
|**update_referential_action_desc**|**nvarchar(60)**|Descrição da ação referencial declarada para esse FOREIGN KEY quando ocorre uma atualização:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = o nome foi gerado pelo sistema.<br /><br /> 0 = O nome foi fornecido pelo usuário.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
