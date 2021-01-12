---
description: sys.destination_data_spaces (Transact-SQL)
title: sys.destination_data_spaces (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.destination_data_spaces
- destination_data_spaces_TSQL
- destination_data_spaces
- sys.destination_data_spaces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.destination_data_spaces catalog view
ms.assetid: 92df932b-ad5c-43f8-81f4-b158823ab189
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d5f3134b70aff51b4e3d91361bb5dacb6cb14f92
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093110"
---
# <a name="sysdestination_data_spaces-transact-sql"></a>sys.destination_data_spaces (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada destino de espaço de dados de um esquema de partição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_scheme_id**|**int**|ID do esquema de partição que está particionando o espaço de dados.|  
|**destination_id**|**int**|ID (de base 1 ordinal) do mapeamento de destino, exclusivo no esquema de partição.|  
|**data_space_id**|**int**|ID do espaço de dados para o qual estão sendo mapeados os dados desse destino de esquema.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
