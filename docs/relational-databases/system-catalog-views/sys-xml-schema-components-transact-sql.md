---
title: sys. xml_schema_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 7b9ab66e0a25067440a496c6c5eb04b5d8b61e64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68039284"
---
# <a name="sysxml_schema_components-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por componente de um esquema XML. O par (**collection_id**, **namespace_id**) é uma chave estrangeira composta para o namespace que a contém. Para componentes nomeados, os valores para **symbol_space**, **Name**, **scoping_xml_component_id**, **is_qualified**, **xml_namespace_id**, **xml_collection_id** são exclusivos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID exclusiva do componente de esquema XML no banco de dados.|  
|**xml_collection_id**|**int**|ID da coleção de esquema XML que contém o namespace desse componente.|  
|**xml_namespace_id**|**int**|ID do namespace XML na coleção.|  
|**is_qualified**|**bit**|1 = Este componente tem um qualificador de namespace explícito.<br /><br /> 0 = É um componente com escopo local. Nesse caso, o par, **namespace_id**, **collection_id**, refere-se ao **targetNamespace**"no namespace".<br /><br /> Para componentes curinga, esse valor será igual a 1.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|Nome exclusivo do componente de esquema XML. Será NULL se o componente não for nomeado.|  
|**symbol_space**|**Char (1)**|Espaço no qual este nome de símbolo é exclusivo, com base no **tipo**:<br /><br /> N = Nenhum<br /><br /> T = Tipo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelo<br /><br /> A = Atributo<br /><br /> G = Grupo de atributo|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Descrição do espaço em que este nome de símbolo é exclusivo, com base no **tipo**:<br /><br /> Nenhuma<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**quase**|**Char (1)**|Tipo de componente de esquema XML.<br /><br /> N = Qualquer tipo (componente intrínseco especial)<br /><br /> Z = Qualquer tipo simples (componente intrínseco especial)<br /><br /> P = Tipo primitivo (tipos intrínsecos)<br /><br /> S = Tipo simples<br /><br /> L = Tipo de lista<br /><br /> U = Tipo de união<br /><br /> C = Tipo simples complexo (derivado de Simples)<br /><br /> K = Tipo complexo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelo<br /><br /> W = Curinga de elemento<br /><br /> A = Atributo<br /><br /> G = Grupo de atributo<br /><br /> V = Curinga de atributo|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Descrição do tipo de componente de esquema XML:<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivação**|**Char (1)**|Método de derivação para tipos derivados:<br /><br /> N = Nenhum (não derivado)<br /><br /> X= Extensão<br /><br /> R = Restrição<br /><br /> S = Substituição|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Descrição de método de derivação para tipos derivados:<br /><br /> Nenhuma<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|ID do componente do qual esse componente é derivado. NULL se não existir nenhuma.|  
|**scoping_xml_component_id**|**int**|ID exclusiva do componente de escopo. NULL se não existir nenhuma (escopo global).|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;o sistema de tipo XML&#41; exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
