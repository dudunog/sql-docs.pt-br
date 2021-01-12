---
description: dbo.sysjobsteps (Transact-SQL)
title: dbo.sysJobSteps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
author: cawrites
ms.author: chadam
ms.openlocfilehash: a3f59ef0d9a3e2a38a7834ed4395319ec935fc59
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98102123"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém as informações de cada etapa em um trabalho a ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**step_id**|**int**|ID da etapa no trabalho.|  
|**step_name**|**sysname**|Nome da etapa do trabalho.|  
|**subsistema**|**nvarchar(40)**|Nome do subsistema usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar a etapa de trabalho.|  
|**command**|**nvarchar(max)**|Comando a ser executado pelo **subsistema**.|  
|**sinalizadores**|**int**|Reservado.|  
|**additional_parameters**|**ntext**|Reservado.|  
|**cmdexec_success_code**|**int**|Valor de nível de erro retornado pelas etapas do subsistema **CmdExec** para indicar êxito.|  
|**on_success_action**|**tinyint**|Ação a ser executada quando uma etapa é executada com êxito.<br /><br /> **1** = (padrão) sair com êxito<br /><br /> **2** = encerrar com falha<br /><br /> **3** = ir para a próxima etapa<br /><br /> **4** = ir para a etapa _on_success_step_id_|
|**on_success_step_id**|**int**|ID da próxima etapa a ser executada quando uma etapa for executada com êxito.|  
|**on_fail_action**|**tinyint**|Ação a ser executada quando uma etapa não é executada com êxito.<br /><br /> **1** = encerrar com êxito<br /><br /> **2** = (padrão) sair com falha<br /><br /> **3** = ir para a próxima etapa<br /><br /> **4** = ir para a etapa _on_fail_step_id_|
|**on_fail_step_id**|**int**|ID da próxima etapa a ser executada quando uma etapa não for executada com êxito.|  
|**server**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Nome do banco de dados no qual o **comando** será executado se o **subsistema** for TSQL.|  
|**database_user_name**|**sysname**|Nome do usuário de banco de dados cuja conta será usada ao executar a etapa.|  
|**retry_attempts**|**int**|Número de novas tentativas feitas se a etapa apresentar falha.|  
|**retry_interval**|**int**|Quantidade de tempo a ser aguardada entre as novas tentativas.|  
|**os_run_priority**|**int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|Nome do arquivo no qual a saída da etapa é salva quando o **subsistema** é TSQL, PowerShell ou **CmdExec**_._|  
|**last_run_outcome**|**int**|Resultado da execução anterior da etapa do trabalho.<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **2** = repetir<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
|**last_run_duration**|**int**|Duração (hhmmss) da etapa na última vez que foi executada.|  
|**last_run_retries**|**int**|Número de novas tentativas na última execução da etapa do trabalho.|  
|**last_run_date**|**int**|Data (yyyymmdd) da última execução iniciada da etapa.|  
|**last_run_time**|**int**|Hora (yyyymmdd) da última execução iniciada da etapa.|  
|**proxy_id**|**int**|Proxy da etapa do trabalho.|  
|**step_uid**|**uniqueidentifier**|Identificador da etapa do trabalho.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
