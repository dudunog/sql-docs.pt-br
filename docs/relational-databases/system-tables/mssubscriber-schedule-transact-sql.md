---
description: MSsubscriber_schedule (Transact-SQL)
title: MSsubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
author: cawrites
ms.author: chadam
ms.openlocfilehash: fda2701763bc5b58a9936e46773f928b45b0d3d8
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98102699"
---
# <a name="mssubscriber_schedule-transact-sql"></a>MSsubscriber_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsubscriber_schedule** contém agendas de sincronização de mesclagem e transacionais padrão para cada par de Publicador/Assinante. Esta tabela é armazenada no banco de dados de distribuição.  
  
> [!NOTE]
>  Esta tabela do sistema foi preterida e está sendo mantida para dar suporte a versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do Publicador.|  
|**farão**|**sysname**|O nome do Assinante.|  
|**agent_type**|**smallint**|O tipo de agente:<br /><br /> 0 = Distribution Agent.<br /><br /> 1 = Merge Agent.|  
|**frequency_type**|**int**|A frequência de agendamento do Distribution Agent:<br /><br /> **1** = uma vez.<br /><br /> **2** = sob demanda.<br /><br /> **4** = diariamente.<br /><br /> **8** = semanalmente.<br /><br /> **16** = mensalmente.<br /><br /> **32** = relativo mensal.<br /><br /> **64** = inicialização automática.<br /><br /> **128** = recorrente.|  
|**frequency_interval**|**int**|O valor a ser aplicado à frequência definida por **frequency_type**.|  
|**frequency_relative_interval**|**int**|A data do Distribution Agent.<br /><br /> **1** = primeiro.<br /><br /> **2** = segundo.<br /><br /> **4** = terceiro.<br /><br /> **8** = quarto.<br /><br /> **16** = última.|  
|**frequency_recurrence_factor**|**int**|O fator de recorrência usado pelo **frequency_type**.|  
|**frequency_subday**|**int**|Frequência de reagendamento durante o período definido:<br /><br /> **1** = uma vez.<br /><br /> **2** = segundo.<br /><br /> **4** = minuto.<br /><br /> **8** = hora.|  
|**frequency_subday_interval**|**int**|O intervalo para **frequency_subday**.|  
|**active_start_time_of_day**|**int**|A hora de dia do primeiro agendamento do Distribution Agent, formatada como HHMMSS.|  
|**active_end_time_of_day**|**int**|A hora do dia em que o Distribution Agent deixa de ser agendado, formatada como HHMMSS.|  
|**active_start_date**|**int**|A data do primeiro agendamento do Distribution Agent, formatada como AAAAMMDD.|  
|**active_end_date**|**int**|A data em que o Distribution Agent deixa de ser agendado, formatada como AAAAMMDD.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
