---
title: dbo. sysjobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ea2b3196e159b19a1baaa032c622a4cf9132402
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097598"
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena as informações de cada trabalho agendado para ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|A ID exclusiva do trabalho.|  
|**originating_server_id**|**int**|ID do servidor do qual o trabalho originou.|  
|**name**|**sysname**|Nome do trabalho.|  
|**habilitado**|**tinyint**|Indica se o trabalho está habilitado para ser executado.|  
|**ndescrição**|**nvarchar(512)**|Descrição do trabalho.|  
|**start_step_id**|**int**|ID da etapa do trabalho em que a execução deve começar.|  
|**category_id**|**int**|ID da categoria de trabalho.|  
|**owner_sid**|**varbinary (85)**|SID (número de identificação de segurança) do proprietário do trabalho.|  
|**notify_level_eventlog**|**int**|**Bitmask** que indica em quais circunstâncias um evento de notificação deve ser registrado no log de aplicativos do Microsoft Windows:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_email**|**int**|Bitmask indicando sob quais circunstâncias um email de notificação deve ser enviado quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_netsend**|**int**|Bitmask indicando sob quais circunstâncias uma mensagem de rede deve ser enviada quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_page**|**int**|Bitmask indicando sob quais circunstâncias uma página deve ser enviada quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_email_operator_id**|**int**|Nome de email do operador a ser notificado.|  
|**notify_netsend_operator_id**|**int**|ID do computador ou usuário usado ao enviar mensagens de rede.|  
|**notify_page_operator_id**|**int**|ID do computador ou usuário usado ao enviar uma página.|  
|**delete_level**|**int**|**Bitmask** que indica em quais circunstâncias o trabalho deve ser excluído quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**date_created**|**datetime**|Data em que o trabalho foi criado.|  
|**date_modified**|**datetime**|Data em que o trabalho foi modificado pela última vez.|  
|**version_number**|**int**|Versão do trabalho.|  
  
  
