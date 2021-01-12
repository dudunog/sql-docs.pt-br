---
description: DROP QUEUE (Transact-SQL)
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: ead004ad07fbab696e42e5efdefa89a04cc0c2a2
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096926"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Descarta uma fila existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name*  
 O nome do banco de dados que contém a fila a ser descartada. Quando não for fornecido nenhum *database_name*, o padrão será o banco de dados atual.  
  
 *schema_name (object)*  
 O nome do esquema que possui a fila a ser descartada. Quando nenhum *schema_name* for fornecido, ele usará como padrão o esquema padrão do usuário atual.  
  
 *queue_name*  
 O nome da fila a ser descartada.  
  
## <a name="remarks"></a>Comentários  
 Não é possível descartar uma fila se qualquer serviço se referir a ela.  
  
## <a name="permissions"></a>Permissões  
 A permissão para remover uma fila usa como padrão o proprietário da fila, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a fila **ExpenseQueue** do banco de dados atual.  
  
```sql  
DROP QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
