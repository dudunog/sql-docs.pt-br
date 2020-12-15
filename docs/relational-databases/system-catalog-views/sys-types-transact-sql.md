---
description: sys.types (Transact-SQL)
title: sys. Types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09a7add1433bc9eb8184843f24d113e3706a4c36
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475087"
---
# <a name="systypes-transact-sql"></a>sys.types (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada tipo definido pelo usuário e sistema.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do tipo. É exclusivo no esquema.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema interno do tipo.|  
|**user_type_id**|**int**|A ID do tipo É exclusiva no banco de dados. Para tipos de dados do sistema, **user_type_id**  =  **system_type_id**.|  
|**schema_id**|**int**|ID do esquema ao qual o tipo pertence.|  
|**principal_id**|**int**|ID do proprietário individual se diferente do proprietário do esquema. Por padrão, os objetos contidos no esquema pertencem ao proprietário do esquema. No entanto, um proprietário alternativo pode ser especificado usando a instrução ALTER AUTHORIZATION para alterar a propriedade.<br /><br /> NULL se não houver nenhum proprietário individual alternativo.|  
|**max_length**|**smallint**|Comprimento de máximo (em bytes) do tipo.<br /><br /> -1 = o tipo de dados da coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.<br /><br /> Para colunas de **texto** , o valor de **max_length** será 16.|  
|**precisão**|**tinyint**|Precisão máxima do tipo se for numérico; caso contrário, 0.|  
|**scale**|**tinyint**|Escala máxima do tipo se for numérico; caso contrário, 0.|  
|**collation_name**|**sysname**|Nome da ordenação do tipo se baseado em caractere; caso contrário, NULL.|  
|**is_nullable**|**bit**|O tipo permite valor nulo.|  
|**is_user_defined**|**bit**|1 = Tipo definido pelo usuário.<br /><br /> 0 = tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_assembly_type**|**bit**|1 = A implementação do tipo foi definida em um assembly CLR.<br /><br /> 0 = O tipo tem como base um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**default_object_id**|**int**|ID do padrão autônomo que está associado ao tipo usando [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md).<br /><br /> 0 = Não existe padrão.|  
|**rule_object_id**|**int**|ID da regra autônoma que está associada ao tipo usando [sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md).<br /><br /> 0 = Não existe regra.|  
|**is_table_type**|**bit**|Indica que o tipo é uma tabela.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
