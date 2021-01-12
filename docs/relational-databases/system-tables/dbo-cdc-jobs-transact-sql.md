---
description: dbo.cdc_jobs (Transact-SQL)
title: dbo.cdc_jobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
author: cawrites
ms.author: chadam
ms.openlocfilehash: c100dfdaad26065946ccba76907ceb0ac6069d2c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094880"
---
# <a name="dbocdc_jobs-transact-sql"></a>dbo.cdc_jobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Armazena os parâmetros de configuração do Change Data Capture para trabalhos de captura e limpeza. Essa tabela é armazenada no **msdb**.  
  
 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados no qual o trabalho está em execução.|  
|**job_type**|**nvarchar (20)**|O tipo de trabalho, 'captura' ou 'limpeza'.|  
|**job_id**|**uniqueidentifier**|ID exclusivo associado ao trabalho.|  
|**maxtrans**|**int**|O número máximo de transações a serem processadas em cada ciclo de verificação.<br /><br /> **maxtrans** é válido somente para trabalhos de captura.|  
|**maxscans**|**int**|O número máximo de ciclos de exame a executar para extrair todas as linhas do log.  <br /><br /> **maxscans** é válido somente para trabalhos de captura.|  
|**visa**|**bit**|Um sinalizador que indica se o trabalho de captura deve ser executado continuamente (1) ou de uma só vez (0). Para obter mais informações, consulte [sys.sp_cdc_add_job &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).<br /><br /> **contínuo** é válido somente para trabalhos de captura.|  
|**pollinginterval**|**bigint**|O número de segundos entre ciclos de exame de log.<br /><br /> **PollingInterval** é válido somente para trabalhos de captura.|  
|**políticas**|**bigint**|O número de minutos que as linhas de alteração serão retidas em tabelas de alteração.<br /><br /> a **retenção** é válida somente para trabalhos de limpeza.|  
|**threshold**|**bigint**|O número máximo de entradas de exclusão que podem ser excluídas usando uma única instrução na limpeza.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.sp_cdc_add_job ](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.sp_cdc_change_job ](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.sp_cdc_help_jobs ](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.sp_cdc_drop_job ](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
