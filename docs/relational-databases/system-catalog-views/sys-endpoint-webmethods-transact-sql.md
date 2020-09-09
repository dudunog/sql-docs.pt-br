---
description: sys.endpoint_webmethods (Transact-SQL)
title: sys. endpoint_webmethods (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dedd1e20af6eed937efa67d655476efc521f9621
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542543"
---
# <a name="sysendpoint_webmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contém uma linha para o método FOR EACH SOAP definido em um ponto de extremidade HTTP com SOAP habilitado. A combinação de endpoint_id  e colunas de namespace é exclusiva.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|O ID do ponto de extremidade para o qual webmethod está definido.|  
|namespace|**nvarchar (384)**|Namespace do webmethod.|  
|method_alias|**nvarchar (64)**|Alias para o método.<br /><br /> Observação: os [!INCLUDE[tsql](../../includes/tsql-md.md)] identificadores permitem caracteres que não são válidos em nomes de métodos WSDL.<br /><br /> O alias é usado para mapear o nome exposto na descrição de WSDL do ponto de extremidade ao objeto executável [!INCLUDE[tsql](../../includes/tsql-md.md)] subjacente real chamado quando o webmethod é invocado.|  
|object_name|**nvarchar (776)**|O nome de objeto para o qual o webmethod é redirecionado, conforme especificado na opção NAME =. Partes de nome são separadas por um ponto (.) e delimitadas usando colchetes, `[``]` .<br /><br /> O nome do objeto deve ser um nome de três partes, conforme especificado na opção de WSDL.|  
|result_schema|**tinyint**|A opção que determina que, se houver, o XSD seja enviado de volta com uma resposta.<br /><br /> 0 = Nenhum<br /><br /> 1 = Padrão<br /><br /> 2 = Padrão|  
|result_schema_desc|**nvarchar(60)**|A descrição da opção que determina que, se houver, o XSD seja enviado de volta com uma resposta.<br /><br /> Nenhuma<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|Opção que determina como os resultados são formatados na resposta.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = NONE|  
|result_format_desc|**nvarchar(60)**|Descrição da opção que determina como os resultados são formatados na resposta.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> Nenhuma|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
