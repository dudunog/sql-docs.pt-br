---
title: sys. extended_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.extended_properties
- sys.extended_properties_TSQL
- extended_properties
- extended_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_properties catalog view
ms.assetid: 439b7299-dce3-4d26-b1c7-61be5e0df82a
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 35d2682709e1f9d19fe51dfae331e0999c0e3570
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733570"
---
# <a name="extended-properties-catalog-views---sysextended_properties"></a>Exibições de catálogo de propriedades estendidas – sys. extended_properties
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Retorna uma linha para cada propriedade estendida no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|class|**tinyint**|Identifica a classe do item no qual a propriedade está presente. Pode ser um dos seguintes:<br /><br /> 0 = Banco de dados<br /><br /> 1 = Objeto ou coluna<br /><br /> 2 = Parâmetro<br /><br /> 3 = Esquema<br /><br /> 4 = Entidade de banco de dados<br /><br /> 5 = Assembly<br /><br /> 6 = Tipo<br /><br /> 7 = índice<br /><br /> 10 = Coleção de esquema XML<br /><br /> 15 = Tipo de mensagem<br /><br /> 16 = Contrato de serviço<br /><br /> 17 = Serviço<br /><br /> 18 = Associação de serviço remoto<br /><br /> 19 = Rota<br /><br /> 20 = Espaço de dados (grupo de arquivos ou esquema de partição)<br /><br /> 21 = Função de partição<br /><br /> 22 = Arquivo de banco de dados<br /><br /> 27 = Guia de plano|  
|class_desc|**nvarchar(60)**|Descrição da classe na qual a propriedade estendida está presente. Pode ser um dos seguintes:<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> PARÂMETRO<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> INDEX<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> DATASPACE<br /><br /> PARTITION_FUNCTION<br /><br /> DATABASE_FILE<br /><br /> PLAN_GUIDE|  
|major_id|**int**|ID do item no qual a propriedade estendida está presente, interpretada de acordo com sua classe. Para a maioria dos itens, essa é a ID que se aplica ao que a classe representa. A interpretação dos principais IDs não padrão é a seguinte:<br /><br /> Se a classe for 0, major_id será sempre 0.<br /><br /> Se a classe for 1, 2 ou 7, major_id será object_id.|  
|minor_id|**int**|ID secundária do item no qual a propriedade estendida está presente, interpretada de acordo com sua classe. Para a maioria dos itens, é 0; caso contrário, a ID será como se segue:<br /><br /> Se class = 1, minor_id será column_id se for coluna, ou 0 se for objeto.<br /><br /> Se class = 2, minor_id será parameter_id.<br /><br /> Se classe 7 = minor _id será index_id.|  
|name|**sysname**|Nome de propriedade exclusivo com class, major_id e minor_id.|  
|value|**sql_variant**|Valor da propriedade estendida.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de propriedades estendidas &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)   
 [sys. fn_listextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addextendedproperty](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropextendedproperty](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
