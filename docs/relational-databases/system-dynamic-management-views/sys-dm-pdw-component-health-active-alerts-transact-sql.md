---
description: sys.dm_pdw_component_health_active_alerts (Transact-SQL)
title: sys.dm_pdw_component_health_active_alerts (Transact-SQL
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: e73c8ea75b6a3613865eb16cd203b207452bfd20
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101400"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Armazena alertas ativos em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componentes.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Confira [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_id|**int**|A ID do tipo de alerta. Confira [sys.pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|Identifica uma instância de um determinado alerta.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|current_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status atual do componente. O valor é nulo para alertas do tipo limite. Consulte [sys.pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|previous_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status do componente anterior. O valor é nulo para alertas do tipo limite. Consulte [sys.pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|create_time|**datetime**|Hora e data em que o alerta foi gerado.|NOT NULL|  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte "valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
