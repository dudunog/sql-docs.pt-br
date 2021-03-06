---
description: sp_reinitmergepullsubscription (Transact-SQL)
title: sp_reinitmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 06b65044129dd302d516eabe3b9c13f6352d3035
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364796"
---
# <a name="sp_reinitmergepullsubscription-transact-sql"></a>sp_reinitmergepullsubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Marca uma assinatura pull de mesclagem para reinicialização, na próxima execução do Agente de Mesclagem. Esse procedimento armazenado é executado no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitmergepullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador* é **sysname** , com um padrão de todos.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db* é **sysname** , com um padrão de todos.  
  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname** , com um padrão de todos.  
  
`[ @upload_first = ] 'upload_first'` É se as alterações no Assinante são carregadas antes da reinicialização da assinatura. *upload_first* é **nvarchar (5)** , com um padrão de false. Se **for true** , as alterações serão carregadas antes que a assinatura seja reinicializada. Se **for false** , as alterações não serão carregadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_reinitmergepullsubscription** é usado na replicação de mesclagem.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
## <a name="examples"></a>Exemplos  

### <a name="a-reinitialize-the-pull-subscription-and-lose-pending-changes"></a>a. Reinicializar a assinatura pull e perder as alterações pendentes

[!code-sql[HowTo#sp_reinitmergepullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_1.sql)]  
  
### <a name="b-reinitialize-the-pull-subscription-and-upload-pending-changes"></a>B. Reinicializar a assinatura pull e carregar alterações pendentes

 [!code-sql[HowTo#sp_reinitmergepullsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_reinitmergepullsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
