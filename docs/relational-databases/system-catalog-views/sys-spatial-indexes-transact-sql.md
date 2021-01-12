---
description: sys.spatial_indexes (Transact-SQL)
title: sys.spatial_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 22d70c60c3234e57cff277e1ba298da9f55148ff
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093010"
---
# <a name="sysspatial_indexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Representa as principais informações dos índices espaciais.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||Herda colunas de [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|spatial_index_type|**tinyint**|Tipo de índice espacial:<br /><br /> 1 = Índice espacial geométrico<br /><br /> 2 = Índice espacial geográfico|  
|spatial_index_type_desc|**nvarchar(60)**|Descrição do tipo de índice espacial:<br /><br /> GEOMETRY = Índice espacial geométrico<br /><br /> GEOGRAPHY = Índice espacial geográfico|  
|tessellation_scheme|**sysname**|Nome do esquema de mosaico:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> Observação: para obter informações sobre esquemas de mosaico, consulte [visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).|  
|\<inherited columns>||Herda colunas de [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).<br /><br /> As colunas herdadas has_filter and filter_definition são exibidas depois das colunas que são específicas para índices espaciais.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
