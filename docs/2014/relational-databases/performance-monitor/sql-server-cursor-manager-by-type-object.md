---
title: SQL Server, objeto Gerenciador de cursor por tipo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 19357f30914ab490d7890f267200b461ffe48cc6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84998103"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server, objeto Cursor Manager by Type
  O objeto **SQLServer:Gerenciador de Cursor por Tipo** fornece contadores para monitorar cursores, agrupados por tipo.  
  
 Esta tabela descreve os contadores do **Gerenciador de Cursor por Tipo** do SQL Server.  
  
|Contadores do Gerenciador de Cursor por Tipo|DESCRIÇÃO|  
|-------------------------------------|-----------------|  
|**Cursores ativos**|Número de cursores ativos.|  
|**Taxa de Acertos do Cache**|Taxa entre acertos e pesquisas do cache.|  
|**Contagens de Cursor em Cache**|Número de cursores de um determinado tipo no cache.|  
|**Contagem de Uso de Cache de Cursor/s**|Número de vezes em que cada tipo de cursor em cache foi usado.|  
|**Uso de memória do cursor**|Quantidade de memória consumida por cursores, em quilobytes (KB).|  
|**Solicitações de Cursor/s**|Número de solicitações de cursor SQL recebidas por servidor.|  
|**Uso de tabelas de trabalho do cursor**|Número de tabelas de trabalho usadas por cursores.|  
|**Número de planos de cursor ativos**|Número de planos de cursor.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância do Gerenciador de Cursor|Descrição|  
|-----------------------------|-----------------|  
|**_Total**|Informações de todos os cursores.|  
|**Cursor API**|Apenas informações de cursor de API.|  
|**Cursor Global de TSQL**|Apenas informações de cursor global de [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**Cursor Local de TSQL**|Apenas informações do cursor local de [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
