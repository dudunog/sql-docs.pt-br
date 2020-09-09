---
description: sp_helpmergepullsubscription (Transact-SQL)
title: sp_helpmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b74d9846d672a59adbde9eada760af1d60fc725e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543265"
---
# <a name="sp_helpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre assinaturas pull que existem em um Assinante. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>Argumento  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** . Se a *publicação* for **%** , as informações sobre todas as publicações de mesclagem e assinaturas no banco de dados atual serão retornadas.  
  
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador*é **sysname**, com um padrão de **%** .  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db*é **sysname**, com um padrão de **%** .  
  
`[ @subscription_type = ] 'subscription_type'` Indica se as assinaturas pull devem ser mostradas. *subscription_type*é **nvarchar (10)**, com um padrão de **' pull '**. Os valores válidos são **' push '**, **' pull '** ou **' both '**.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|O nome da assinatura.|  
|**documento**|**sysname**|Nome da publicação.|  
|**programa**|**sysname**|Nome do Publicador.|  
|**publisher_db**|**sysname**|Nome do banco de dados do Publicador.|  
|**farão**|**sysname**|Nome do Assinante.|  
|**subscription_db**|**sysname**|Nome do banco de dados de assinatura.|  
|**status**|**int**|O status da assinatura:<br /><br /> **0** = assinatura inativa<br /><br /> **1** = assinatura ativa<br /><br /> **2** = assinatura excluída<br /><br /> **3** = assinatura desanexada<br /><br /> **4** = assinatura anexada<br /><br /> **5** = a assinatura foi marcada para reinicialização com upload<br /><br /> **6** = falha na anexação da assinatura<br /><br /> **7** = assinatura restaurada do backup|  
|**subscriber_type**|**int**|O tipo de Assinante:<br /><br /> **1** = global<br /><br /> **2** = local<br /><br /> **3** = anônimo|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = enviar por push<br /><br /> **1** = pull<br /><br /> **2** = anônimo|  
|**priority**|**float (8)**|A prioridade da assinatura. O valor deve ser menor que **100, 0**.|  
|**sync_type**|**tinyint**|O tipo de sincronização da assinatura:<br /><br /> **1** = automático<br /><br /> **2** = o instantâneo não é usado.|  
|**descrição**|**nvarchar(255)**|Uma descrição breve da assinatura pull.|  
|**merge_jobid**|**binary(16)**|ID do trabalho do Agente de Mesclagem.|  
|**enabled_for_syncmgr**|**int**|Se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização da [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**last_updated**|**nvarchar (26)**|Hora da última sincronização bem-sucedida da assinatura pelo Merge Agent.|  
|**publisher_login**|**sysname**|O nome de logon do Publicador.|  
|**publisher_password**|**sysname**|A senha do Publicador.|  
|**publisher_security_mode**|**int**|Especifica o modo de segurança do Publicador:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**distribuidor**|**sysname**|Nome do Distribuidor.|  
|**distributor_login**|**sysname**|O nome de logon do Distribuidor.|  
|**distributor_password**|**sysname**|A senha do Distribuidor.|  
|**distributor_security_mode**|**int**|Especifica o modo de segurança do Distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**ftp_address**|**sysname**|Disponível somente para compatibilidade com versões anteriores. É o endereço de rede do serviço FTP (File Transfer Protocol) para o distribuidor.|  
|**ftp_port**|**int**|Disponível somente para compatibilidade com versões anteriores. É o número da porta do serviço FTP para o Distribuidor.|  
|**ftp_login**|**sysname**|Disponível somente para compatibilidade com versões anteriores. É o nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**sysname**|Disponível somente para compatibilidade com versões anteriores. É a senha de usuário usada para se conectar ao serviço FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Local onde a pasta de instantâneo é armazenada se o local for diferente ou for uma adição ao local padrão.|  
|**working_directory**|**nvarchar(255)**|Caminho completamente qualificado para o diretório onde os arquivos de instantâneo são transferidos usando o FTP quando essa opção é especificada.|  
|**use_ftp**|**bit**|A assinatura está assinando a publicação pela Internet e as propriedades de endereçamento do FTP estão configuradas. Se **0**, a assinatura não está usando o FTP. Se **1**, a assinatura está usando FTP.|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado e executado remotamente. Se for **0**, o agente não poderá ser ativado remotamente.|  
|**offload_server**|**sysname**|O nome do servidor usado para ativação remota.|  
|**use_interactive_resolver**|**int**|Retorna se o resolvedor interativo é usado ou não durante a reconciliação. Se for **0**, o resolvedor interativo não será usado.|  
|**subid**|**uniqueidentifier**|A ID do Assinante.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|O caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**last_sync_status**|**int**|O status de sincronização:<br /><br /> **1** = Iniciando em<br /><br /> **2** = com êxito<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetindo após uma falha anterior<br /><br /> **6** = com falha<br /><br /> **7** = falha na validação<br /><br /> **8** = validação aprovada<br /><br /> **9** = desligamento solicitado|  
|**last_sync_summary**|**sysname**|Descrição dos últimos resultados da sincronização.|  
|**use_web_sync**|**bit**|Especifica se a assinatura pode ser sincronizada via HTTPS, em que o valor **1** significa que esse recurso está habilitado.|  
|**internet_url**|**nvarchar(260)**|URL que representa o local do Replication Listener para sincronização da Web.|  
|**internet_login**|**nvarchar(128)**|Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**|**nvarchar (524)**|Senha para o logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**int**|O modo de autenticação usado para se conectar ao servidor da Web que está hospedando a sincronização da Web. Um valor de **1** significa autenticação do Windows e um valor de **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**internet_timeout**|**int**|Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**hostname**|**nvarchar(128)**|Especifica um valor sobrecarregado para [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) quando essa função é usada na cláusula WHERE de um filtro de linha com parâmetros.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows na qual o Merge Agent é executado, que é retornado no formato *domínio* \\ *nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de " **\*\*\*\*\*\*\*\*\*\*** " é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergepullsubscription** é usado na replicação de mesclagem. No conjunto de resultados, a data retornada em **Last_updated** é formatada como *aaaammdd hh: mm: SS. FFF*.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_helpmergepullsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addmergepullsubscription ](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepullsubscription ](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepullsubscription ](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
