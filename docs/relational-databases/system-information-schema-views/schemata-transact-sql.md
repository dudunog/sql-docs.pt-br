---
title: SCHEMATA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a257a28a51a9e54643b14e57ff8c778179ee3bd7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716627"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Retorna uma linha para cada esquema no banco de dados atual. Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_. Para recuperar informações sobre todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte a exibição de catálogo de [&#41;do sys. databases &#40;TRANSACT-SQL](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|Nome do banco de dados atual|  
|**SCHEMA_NAME**|**nvarchar (** 128 **)**|Retorna o nome do esquema.|  
|**SCHEMA_OWNER**|**nvarchar (** 128 **)**|Nome do proprietário do esquema.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição do catálogo sys.objects.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|Retorna o nome do conjunto de caracteres padrão.|  

**Exemplo**  
O exemplo a seguir retorna informações sobre os esquemas no banco de dados mestre:  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
