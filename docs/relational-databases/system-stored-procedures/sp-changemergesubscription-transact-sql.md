---
title: sp_changemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3f7597272a1547a11f2c76e65fab391e2fbcd05
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829579"
---
# <a name="sp_changemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades selecionadas de uma assinatura push de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação a ser alterada. a *publicação* é **sysname**, com um padrão de NULL. A publicação já deve existir e ser adequada às regras para identificadores.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db*é **sysname**, com um padrão de NULL.  
  
`[ @property = ] 'property'`É a propriedade a ser alterada para a publicação fornecida. a *Propriedade* é **sysname**e pode ser um dos valores na tabela.  
  
`[ @value = ] 'value'`É o novo valor para a *Propriedade*especificada. o *valor* é **nvarchar (255)** e pode ser um dos valores na tabela.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**ndescrição**||Descrição da assinatura de mesclagem.|  
|**prioridade**||É a prioridade da assinatura. A prioridade é usada pelo resolvedor padrão para escolher um vencedor quando são detectados conflitos.|  
|**merge_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**publisher_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador.|  
|**publisher_login**||Nome de logon no Publicador.|  
|**publisher_password**||Senha forte para o logon do Publicador fornecido.|  
|**subscriber_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Assinante.|  
||**0**|Use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Assinante.|  
|**subscriber_login**||Nome de logon no Assinante.|  
|**subscriber_password**||Senha forte para o logon de Assinante fornecido.|  
|**sync_type**|**Automático**|Esquema e dados iniciais de tabelas publicadas são transferidos ao Assinante primeiro.|  
||**nenhum**|O Assinante já tem o esquema e os dados iniciais para as tabelas publicadas; tabelas de sistema e dados são sempre transferidos.|  
|**use_interactive_resolver**|**true**|Permite resolver conflitos interativamente para todos os artigos que permitem resolução interativa.|  
||**false**|Conflitos são resolvidos automaticamente usando um resolvedor padrão ou resolvedor personalizado.|  
|NULL (padrão)|NULL (padrão)||  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergesubscription** é usado na replicação de mesclagem.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changemergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergesubscription](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
