---
description: sp_help_targetserver (Transact-SQL)
title: sp_help_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02304ff4c41f45e90c24fb4be1a815be49c1336a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527323"
---
# <a name="sp_help_targetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lista todos os servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server_name'` O nome do servidor para o qual retornar informações. *server_name* é **nvarchar (30)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *server_name* não for especificado, **sp_help_targetserver** retornará esse conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Número de identificação do servidor.|  
|**server_name**|**nvarchar(30)**|Nome de servidor.|  
|**local**|**nvarchar(200)**|Localização do servidor especificado.|  
|**time_zone_adjustment**|**int**|Ajuste de fuso horário, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data do alistamento do servidor especificado.|  
|**last_poll_date**|**datetime**|Data da última vez em que o servidor foi  sondado para trabalhos.|  
|**status**|**int**|Status do servidor especificado.|  
|**unread_instructions**|**int**|Indica se o servidor tem ordens não lidas. Se todas as linhas tiverem sido baixadas, essa coluna será **0**.|  
|**local_time**|**datetime**|Data e hora locais do servidor de destino, baseadas na hora local do servidor de destino até a última sondagem do servidor mestre.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|Usuário de Microsoft Windows que inscreveu o servidor de destino.|  
|**poll_interval**|**int**|Frequência em segundos com que o servidor de destino sonda o serviço Master SQLServer Agent para baixar trabalhos e carregar o status dos trabalhos.|  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>a. Listando informações para todos os servidores de destino registrados  
 O exemplo a seguir lista as informações de todos os servidores de destino registrados.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. Listando informações de um servidor de destino específico.  
 O exemplo a seguir lista as informações do servidor de destino `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_targetservergroup ](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_targetserver ](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_targetservergroup ](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_targetservergroup ](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
