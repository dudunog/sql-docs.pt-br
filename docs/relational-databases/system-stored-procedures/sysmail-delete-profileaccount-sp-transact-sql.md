---
title: sysmail_delete_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
author: stevestein
ms.author: sstein
ms.openlocfilehash: cf2e5f7e05286da23f4bccc94d1017f00cb7db70
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67909192"
---
# <a name="sysmail_delete_profileaccount_sp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma conta de um perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`A ID de perfil do perfil a ser excluído. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou o *profile_name* pode ser especificado.  
  
`[ @profile_name = ] 'profile_name'`O nome do perfil do perfil a ser excluído. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou o *profile_name* pode ser especificado.  
  
`[ @account_id = ] account_id`A ID da conta a ser excluída. *account_id* é **int**, com um padrão de NULL. O *account_id* ou o *account_name* pode ser especificado.  
  
`[ @account_name = ] 'account_name'`O nome da conta a ser excluída. *account_name* é **sysname**, com um padrão de NULL. O *account_id* ou o *account_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Retorna um erro se a conta especificada não estiver associada ao perfil especificado.  
  
 Quando é especificada uma conta, mas não um perfil, esse procedimento armazenado remove a conta especificada de todos os perfis. Por exemplo, se você estiver se preparando para desligar um servidor SMTP existente, deverá remover as contas que usam esse servidor SMTP de todos os perfis, em vez de remover cada conta de cada perfil.  
  
 Quando um perfil é especificado, mas não uma conta, esse procedimento armazenado remove todas as contas do perfil especificado. Por exemplo, se você estiver alterando os servidores SMTP que um perfil utiliza, pode ser conveniente remover todas as contas do perfil e, depois, adicionar novas contas conforme necessário.  
  
 O procedimento armazenado **sysmail_delete_profileaccount_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a remoção da conta `Audit Account` do perfil `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
