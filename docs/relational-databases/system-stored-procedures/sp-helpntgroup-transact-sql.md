---
description: sp_helpntgroup (Transact-SQL)
title: sp_helpntgroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpntgroup
- sp_helpntgroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpntgroup
ms.assetid: 02b4f7c1-480a-436c-8bae-7a2488be45d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a88caee8d332a4802f4281360f93392ae29aa2c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535156"
---
# <a name="sp_helpntgroup-transact-sql"></a>sp_helpntgroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Reporta informações sobre grupos do Windows com contas no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpntgroup [ [ @ntname= ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ntname = ] 'name'` É o nome do grupo do Windows. o *nome* é **sysname**, com um padrão de NULL. o *nome* deve ser um grupo válido do Windows com acesso ao banco de dados atual. Se o *nome* não for especificado, todos os grupos do Windows com acesso ao banco de dados atual serão incluídos na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**NTGroupName**|**sysname**|Nome do grupo do Windows.|  
|**NTGroupId**|**smallint**|Identificador de grupo (ID).|  
|**SID**|**varbinary(85)**|SID (identificador de segurança) de **NTGroupName**.|  
|**HasDbAccess**|**int**|1 = grupo do Windows tem permissão para acessar o banco de dados.|  
  
## <a name="remarks"></a>Comentários  
 Para ver uma lista das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções no banco de dados atual, use **sp_helprole**.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir imprime uma lista dos grupos do Windows com acesso ao banco de dados atual.  
  
```  
EXEC sp_helpntgroup;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprole ](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
