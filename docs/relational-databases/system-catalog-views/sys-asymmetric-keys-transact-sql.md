---
description: sys.asymmetric_keys (Transact-SQL)
title: sys.asymmetric_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- asymmetric_keys
- sys.asymmetric_keys_TSQL
- asymmetric_keys_TSQL
- sys.asymmetric_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.asymmetric_keys catalog view
ms.assetid: bbca796a-9bb5-4a62-9ca8-1d255984553d
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf926f7c3d3ab84a41ed142dd8ff1bef7357af96
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091523"
---
# <a name="sysasymmetric_keys-transact-sql"></a>sys.asymmetric_keys (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada chave assimétrica.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da chave. É exclusiva no banco de dados.|  
|**principal_id**|**int**|ID da entidade de banco de dados que possui a chave.|  
|**asymmetric_key_id**|**int**|ID da chave. É exclusiva no banco de dados.|  
|**pvt_key_encryption_type**|**char(2)**|Como a chave é criptografada.<br /><br /> NA = Não criptografada<br /><br /> MK = A chave é criptografada pela chave mestra<br /><br /> PW = A chave é criptografada por uma senha definida pelo usuário<br /><br /> SK = A chave é criptografada pela chave mestra de serviço.|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Descrição de como a chave privada é criptografada.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**digitais**|**varbinary(32)**|Hash SHA-1 da chave. O hash é globalmente exclusivo.|  
|**algoritmo**|**char(2)**|Algoritmo usado com a chave.<br /><br /> 1R = RSA de 512 bits<br /><br /> 2R = RSA de 1024 bits<br /><br /> 3R = RSA de 2048 bits|  
|**algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo usado com a chave.<br /><br /> RSA_512<br /><br /> RSA_1024<br /><br /> RSA_2048|  
|**key_length**|**int**|Comprimento de bit da chave.|  
|**SIDs**|**varbinary(85)**|SID de logon para essa chave. Para chaves de Gerenciamento de Chave Extensível, esse valor será NULL.|  
|**string_sid**|**nvarchar(128)**|Representação de cadeia de caracteres do SID de logon da chave. Para chaves de Gerenciamento de Chave Extensível, esse valor será NULL.|  
|**public_key**|**varbinary(max)**|Chave pública.|  
|**attested_by**|**nvarchar(260)**|Somente para uso do sistema.|  
|**provider_type**|**nvarchar(120)**|Tipo de provedor criptográfico:<br /><br /> CRYPTOGRAPHIC PROVIDER = Chaves de Gerenciamento de Chave Extensível<br /><br /> NULL = Chaves de Gerenciamento de Chave não Extensível|  
|**cryptographic_provider_guid**|**uniqueidentifier**|GUID do provedor criptográfico. Para chaves de Gerenciamento de Chave não Extensível, esse valor será NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|ID de algoritmo do provedor criptográfico. Para chaves de Gerenciamento de Chave não Extensível, esse valor será NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
  
