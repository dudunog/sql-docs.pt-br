---
description: sp_dropdistpublisher (Transact-SQL)
title: sp_dropdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2d7d0eed28b877c881cd297556755ea70bf5c674
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543501"
---
# <a name="sp_dropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Descarta um Publicador de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o Publicador a ser solto. o *Publicador* é **sysname**, sem padrão.  
  
`[ @no_checks = ] no_checks` Especifica se **sp_dropdistpublisher** verifica se o Publicador desinstalou o servidor como o distribuidor. *no_checks* é **bit**, com um padrão de **0**.  
  
 Se **0**, a replicação verifica se o Publicador remoto desinstalou o servidor local como o distribuidor. Se o Publicador for local, a replicação verificará se não há objetos de publicação ou distribuição restantes no servidor local.  
  
 Se **1**, todos os objetos de replicação associados ao Publicador de distribuição serão removidos mesmo que um Publicador remoto não possa ser acessado. Depois de fazer isso, o Publicador remoto deve desinstalar a replicação usando [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) com ** \@ ignore_distributor**  =  **1**.  
  
`[ @ignore_distributor = ] ignore_distributor` Especifica se os objetos de distribuição são deixados no distribuidor quando o Publicador é removido. *ignore_distributor* é **bit** e pode ser um destes valores:  
  
 **1** = os objetos de distribuição que pertencem ao *Publicador* permanecem no distribuidor.  
  
 **0** = os objetos de distribuição para o *Publicador* são limpos no distribuidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropdistpublisher** é usado em todos os tipos de replicação.  
  
 Ao remover um Publicador Oracle, se não for possível descartar o Publicador **sp_dropdistpublisher** retornará um erro e os objetos do distribuidor para o Publicador serão removidos.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_dropdistpublisher**.  
  
## <a name="see-also"></a>Consulte Também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [&#41;&#40;Transact-SQL de sp_adddistpublisher ](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
