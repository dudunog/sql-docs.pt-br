---
title: sp_syspolicy_delete_policy_execution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cbee07cd02ca423a633133546130615bcb1d60c1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892714"
---
# <a name="sp_syspolicy_delete_policy_execution_history-transact-sql"></a>sp_syspolicy_delete_policy_execution_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui o histórico de execução de políticas no Gerenciamento Baseado em Políticas. Você pode usar este procedimento armazenado para excluir o histórico de execução de uma política específica ou de todas as políticas e excluir o histórico de execução antes de uma data específica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @policy_id = ] policy_id`É o identificador da política para a qual você deseja excluir o histórico de execução. *policy_id* é **int**e é obrigatório. Pode ser NULL.  
  
`[ @oldest_date = ] 'oldest_date'`É a data mais antiga para a qual você deseja manter o histórico de execução da política. Qualquer histórico de execução anterior a essa data será excluído. *oldest_date* é **DateTime**e é obrigatório. Pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_delete_policy_execution_history no contexto do banco de dados de sistema msdb.  
  
 Para obter valores para *policy_id*e exibir datas do histórico de execução, você pode usar a seguinte consulta:  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 O comportamento a seguir será aplicado se você especificar NULL para obter um ou ambos valores:  
  
-   Para excluir todo o histórico de execução de política, especifique NULL para *policy_id* e para *oldest_date*.  
  
-   Para excluir todo o histórico de execução de política de uma política específica, especifique um identificador de política para *policy_id*e especifique NULL como *oldest_date*.  
  
-   Para excluir o histórico de execução de política para todas as políticas antes de uma data específica, especifique NULL para *policy_id*e especifique uma data para *oldest_date*.  
  
 Para arquivar o histórico de execução de política, você pode abrir o log Histórico de Política no Pesquisador de Objetos e exportar o histórico de execução para um arquivo. Para acessar o log de histórico de política, expanda **Gerenciamento**, clique com o botão direito do mouse em **Gerenciamento de política**e clique em **Exibir histórico**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte exclui o histórico de execução de política anterior a uma data específica de uma política com ID 7.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syspolicy_set_config_history_retention](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syspolicy_purge_history](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
