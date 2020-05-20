---
title: sp_dropsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2f800ef185145e63a17db3855989bebde91b48bc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831140"
---
# <a name="sp_dropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Descarta assinaturas para um artigo específico, publicação ou conjunto de assinaturas no Publicador. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação associada. a *publicação* é **sysname**, com um padrão de NULL. Se **todas**, todas as assinaturas de todas as publicações para o assinante especificado serão canceladas. a *publicação* é um parâmetro necessário.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, com um valor padrão de NULL. Se **todas as**assinaturas, todos os artigos de cada publicação e assinante especificados forem removidos. Use **tudo** para publicações que permitem atualização imediata.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante que terá suas assinaturas descartadas. o *assinante* é **sysname**, sem padrão. Se **todas**, todas as assinaturas de todos os assinantes forem descartadas.  
  
`[ @destination_db = ] 'destination_db'`É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de NULL. Se for NULL, todas as assinaturas daquele Assinante serão descartadas.  
  
`[ @ignore_distributor = ] ignore_distributor`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @reserved = ] 'reserved'`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropsubscription** é usado em instantâneo e replicação transacional.  
  
 Se você descartar a assinatura de um artigo em uma publicação de sincronização imediata, não poderá adicioná-la novamente, exceto se descartar as assinaturas em todos os artigos de publicação e os adicionar novamente, todos de uma vez.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** ou o usuário que criou a assinatura podem executar **sp_dropsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma assinatura push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changesubstatus](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
