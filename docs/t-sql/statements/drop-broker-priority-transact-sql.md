---
description: DROP BROKER PRIORITY (Transact-SQL)
title: DROP BROKER PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f5645014442ddeda800fdb5570ff76a96e943f62
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095743"
---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove uma prioridade de conversa do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *ConversationPriorityName*  
 Especifica o nome da prioridade de conversa a ser removido.  
  
## <a name="remarks"></a>Comentários  
 Quando você descarta uma prioridade de conversa, as conversas existentes continuam a funcionar com os níveis de prioridade atribuídos a partir da prioridade de conversa.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar uma prioridade de conversa assume como padrão os membros das funções de banco de dados fixas db_ddladmin ou db_owner e a função de servidor fixa sysadmin. Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta a prioridade de conversa denominada `InitiatorAToTargetPriority`.  
  
```sql  
DROP BROKER PRIORITY InitiatorAToTargetPriority;
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
