---
description: syscollector_collection_items (Transact-SQL)
title: syscollector_collection_items (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 79b0c876d8c42cd23f02e91dead3fde841d84f07
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094273"
---
# <a name="syscollector_collection_items-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre um item em um conjunto de coleta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|Identifica o conjunto de coleta. Não permite valor nulo.|  
|**collection_item_id**|**int**|Identifica um item no conjunto de coleta. Não permite valor nulo.|  
|**collector_type_uid**|**uniqueidentifier**|GUID usado para identificar o tipo de coletor. Não permite valor nulo.|  
|**name**|**nvarchar(4000)**|Nome do conjunto de coleta. Permite valor nulo.|  
|**frequência**|**int**|Frequência com que os dados são coletados por um item de coleta. Não permite valor nulo.|  
|**parameters**|**xml**|Descreve a parametrização para o tipo de coletor associado ao item de coleta. O esquema XML para esse item de coleta é validado com o esquema XML (XSD) armazenado no **parameter_schema** para um tipo de coletor específico. Permite valor nulo. Para obter mais informações, consulte [syscollector_collector_types &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT for **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
