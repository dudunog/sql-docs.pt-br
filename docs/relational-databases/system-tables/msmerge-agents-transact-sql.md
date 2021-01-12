---
description: MSmerge_agents (Transact-SQL)
title: MSmerge_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
author: cawrites
ms.author: chadam
ms.openlocfilehash: 9380cd5c5e04293e0296c098ee7455eb803e3972
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096201"
---
# <a name="msmerge_agents-transact-sql"></a>MSmerge_agents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_agents** contém uma linha para cada agente de mesclagem em execução no Assinante. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do Merge Agent.|  
|**name**|**nvarchar (100)**|O nome do Merge Agent.|  
|**publisher_id**|**smallint**|A ID do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**documento**|**sysname**|O nome da publicação.|  
|**subscriber_id**|**smallint**|A ID do Assinante.|  
|**subscriber_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**local_job**|**bit**|Indica se há um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor local.|  
|**job_id**|**binary(16)**|O número de identificação do trabalho.|  
|**profile_id**|**int**|A ID de configuração da tabela de **MSagent_profiles** .|  
|**anonymous_subid**|**uniqueidentifier**|A ID de um agente anônimo.|  
|**subscriber_name**|**sysname**|O nome do Assinante.|  
|**creation_date**|**datetime**|A data e a hora em que a distribuição ou a Agente de Mesclagem foi criada.|  
|**offload_enabled**|**bit**|Especifica que o agente pode ser ativado remotamente.<br /><br /> **0** especifica que o agente não pode ser ativado remotamente.<br /><br /> **1** especifica se o agente será ativado remotamente e no computador remoto especificado na propriedade offload_server.|  
|**offload_server**|**sysname**|Especifica o nome da rede de servidor a ser usado para ativação de agente remota.|  
|**SIDs**|**varbinary(85)**|O SID (número de identificação de segurança) para o Distribution Agent ou Merge Agent durante sua primeira execução.|  
|**subscriber_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Assinante que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**subscriber_login**|**sysname**|O logon usado na conexão com o Assinante.|  
|**subscriber_password**|**nvarchar (524)**|O valor criptografado da senha usada na conexão com o Assinante.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente na conexão com o Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**publisher_login**|**sysname**|O logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar (524)**|O valor criptografado da senha usada na conexão com o Publicador.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
