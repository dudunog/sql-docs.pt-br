---
description: sp_delete_notification (Transact-SQL)
title: sp_delete_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_notification_TSQL
- sp_delete_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_notification
ms.assetid: b55d3898-596d-47a5-a4f0-d65dc736223b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0f023990f20765272fe2cde09f5599ecf736f076
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546140"
---
# <a name="sp_delete_notification-transact-sql"></a>sp_delete_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove uma definição de notificação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para um alerta e operador específicos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_notification  
     [ @alert_name = ] 'alert' ,   
     [ @operator_name = ] 'operator'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @alert_name = ] 'alert'` O nome do alerta. o *alerta* é **sysname**, sem padrão.  
  
`[ @operator_name = ] 'operator'` O nome do operador. o *operador* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A remoção de uma notificação remove somente a notificação; o alerta e o operador permanecem intactos.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem receber a função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a notificação enviada ao operador `François Ajenstat` quando ocorre o alerta `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_notification  
    @alert_name = 'Test Alert',  
    @operator_name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_notification ](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_operator ](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_alert ](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_alert ](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_notification ](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_operator ](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_notification ](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
