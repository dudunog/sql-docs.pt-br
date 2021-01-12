---
description: dbo.sysjobschedules (Transact-SQL)
title: dbo.sysJobSchedules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3880d33e9c69a4911aa64487c34e636ce45a3a05
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096262"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações de agenda dos trabalhos a serem executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
> **Observação:** A tabela **sysjobschedules** é atualizada a cada 20 minutos, o que pode afetar os valores retornados pelo procedimento armazenado **sp_help_jobschedule** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID da agenda.|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**next_run_date**|**int**|Data e hora para as quais está programada a próxima execução do trabalho. A data é formatada como AAAAMMDD.|  
|**next_run_time**|**int**|Hora em que o trabalho está agendado para ser executado. A hora é formatada como HHMMSS e usa um relógio de 24 horas.|  
  
## <a name="see-also"></a>Consulte Também  
 [ Agendas dedbo.sys&#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
