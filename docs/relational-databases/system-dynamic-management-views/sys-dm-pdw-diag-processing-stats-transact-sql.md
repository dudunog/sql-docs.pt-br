---
description: sys.dm_pdw_diag_processing_stats (Transact-SQL)
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: a50a56e230d4074e567d63bea14744aa4dd18fd6
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98097516"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Exibe informações relacionadas a todos os eventos de diagnóstico internos que podem ser incorporados em sessões de diagnóstico definidas pelo administrador. Consulte esta exibição para entender as estatísticas por trás dos subsistemas de diagnóstico e eventos que orientam a população de todas as outras DMVs. Há um grupo de filas para cada processo em cada nó.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Nó do dispositivo do qual este log se encontra.|  
|**process_id**|**int**|Identificador do processo que executa o envio dessa estatística.|  
|**target_name**|**nvarchar(255)**|O nome da fila.|  
|**queue_size**|**int**|O número de itens na fila de processos. O tamanho da fila geralmente é 0. Um número positivo indica que o sistema está sob estresse e está criando a pendência de eventos. Uma contagem positiva nas outras colunas significa que o sistema se tornou corrompido para essa fila específica e quaisquer DMVs relacionados.|  
|**lost_events_count**|**bigint**|O número de eventos perdidos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
