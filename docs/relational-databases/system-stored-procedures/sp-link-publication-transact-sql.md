---
title: sp_link_publication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 976109aa0ef09575f818ff6daf82e742626dede7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756641"
---
# <a name="sp_link_publication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Define as informações de configuração e de segurança usadas por gatilhos de sincronização de assinaturas de atualização imediata na conexão com o Publicador. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
> [!IMPORTANT]
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
> 
> [!IMPORTANT]
>  Em determinadas condições, esse procedimento armazenado poderá falhar se o Assinante estiver executando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 ou posterior e o Publicador estiver executando uma versão anterior. Se o procedimento armazenado falhar neste cenário, atualize o Publicador para a versão do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 ou posterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador a ser vinculado. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador a ser vinculado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação à qual vincular. a *publicação* é **sysname**, sem padrão.  
  
`[ @security_mode = ] security_mode`É o modo de segurança usado pelo assinante para se conectar a um Publicador remoto para atualização imediata. *security_mode* é **int**e pode ser um desses valores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação com o logon especificado neste procedimento armazenado como *logon* e *senha*.<br /><br /> Observação: em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa opção foi usada para especificar uma RPC (chamada de procedimento remoto) dinâmica.|  
|**1**|Usa o contexto de segurança (Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Autenticação do Windows) do usuário que faz a alteração no Assinante.<br /><br /> Observação: essa conta também deve existir no Publicador com privilégios suficientes. Ao usar Autenticação do Windows, deve haver suporte para delegação de conta de segurança.|  
|**2**|Usa um logon de servidor vinculado existente definido pelo usuário criado usando **sp_link_publication**.|  
  
`[ @login = ] 'login'`É o logon. *login* é **sysname**, com um padrão de NULL. Esse parâmetro deve ser especificado quando *security_mode* é **0**.  
  
`[ @password = ] 'password'`É a senha. a *senha* é **sysname**, com um padrão de NULL. Esse parâmetro deve ser especificado quando *security_mode* é **0**.  
  
`[ @distributor = ] 'distributor'`É o nome do distribuidor. o *distribuidor* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_link_publication** é usado pelas assinaturas de atualização imediata na replicação transacional.  
  
 **sp_link_publication** pode ser usado para assinaturas push e pull. Pode ser chamado antes ou depois que a assinatura é criada. Uma entrada é inserida ou atualizada no [MSsubscription_properties &#40;tabela do sistema&#41;Transact-SQL](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) .  
  
 Para assinaturas push, a entrada pode ser limpa por [sp_subscription_cleanup &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). Para assinaturas pull, a entrada pode ser limpa por [sp_droppullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) ou [sp_subscription_cleanup &#40;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)&#41;. Você também pode chamar **sp_link_publication** com uma senha nula para limpar a entrada no MSsubscription_properties &#40;tabela do sistema [&#41;do Transact-SQL](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) para questões de segurança.  
  
 O modo padrão usado por um Assinante de atualização imediata quando ele se conecta ao Publicador não permite uma conexão usando Autenticação do Windows. Para se conectar ao modo de Autenticação do Windows, um servidor vinculado precisa ser definido como Publicador e o Assinante de atualização imediata deve usar essa conexão ao atualizar o Assinante. Isso requer que o **sp_link_publication** seja executado com *security_mode*  =  **2**. Ao usar Autenticação do Windows, deve haver suporte para delegação de conta de segurança.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_link_publication**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_droppullsubscription](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_subscription_cleanup](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
