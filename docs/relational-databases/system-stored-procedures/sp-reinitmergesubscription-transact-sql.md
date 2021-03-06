---
description: sp_reinitmergesubscription (Transact-SQL)
title: sp_reinitmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bc1d2d3dc8b9763d19410b2a9773fb7766d22140
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364729"
---
# <a name="sp_reinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Marca uma assinatura de mesclagem para reinicialização na próxima execução do Agente de Mesclagem. Esse procedimento armazenado é executado no Publicador do banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname** , com um padrão de **todos**.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname** , com um padrão de **todos**.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados do Assinante. *subscriber_db* é **sysname** , com um padrão de **todos**.  
  
`[ @upload_first = ] 'upload_first'` É se as alterações no Assinante são carregadas antes da reinicialização da assinatura. *upload_first* é **nvarchar (5)** , com um padrão de false. Se **for true** , as alterações serão carregadas antes que a assinatura seja reinicializada. Se **for false** , as alterações não serão carregadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_reinitmergesubscription** é usado na replicação de mesclagem.  
  
 **sp_reinitmergesubscription** pode ser chamado no Publicador para reinicializar assinaturas de mesclagem. Recomendamos reexecutar o Agente de Instantâneo também.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
## <a name="examples"></a>Exemplos  

### <a name="a-reinitialize-the-push-subscription-and-lose-pending-changes"></a>a. Reinicializar a assinatura push e perder as alterações pendentes

 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
### <a name="b-reinitialize-the-push-subscription-and-upload-pending-changes"></a>B. Reinicializar a assinatura push e carregar alterações pendentes
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_reinitmergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
