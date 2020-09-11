---
description: CONTEXT_INFO (Transact-SQL)
title: CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8b4f5b2fa72f6122f457f2b86ccfe7ec399e2bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445856"
---
# <a name="context_info--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função retorna o valor **context_info** definido para a sessão ou lote atual ou derivado por meio do uso da instrução [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONTEXT_INFO()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-value"></a>Retornar valor
O valor **context_info**.
  
Se **context_info** não foi definido:
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], retorna NULL.  
-   Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], retorna um GUID exclusivo específico da sessão.  
  
## <a name="remarks"></a>Comentários  
O recurso MARS (Vários Conjuntos de Resultados Ativos) permite que os aplicativos sejam executados em vários lotes, ou solicitações, ao mesmo tempo na mesma conexão. Quando um dos lotes de conexão MARS executa SET CONTEXT_INFO, a função `CONTEXT_INFO` retorna o valor do novo contexto, quando a função `CONTEXT_INFO` é executada no mesmo lote que a instrução SET. Se a função `CONTEXT_INFO` é executada em um ou mais dos outros lotes de conexão, o `CONTEXT_FUNCTION` não retorna o novo valor, a menos que os lotes iniciados após a conclusão do lote que executou a instrução SET.
  
## <a name="permissions"></a>Permissões  
Não requer nenhuma permissão especial. As seguintes exibições do sistema armazenam as informações de contexto, mas consultar essas exibições diretamente requer permissões SELECT e VIEW SERVER STATE:
- **sys.dm_exec_requests**
- **sys.dm_exec_sessions**
- **sys.sysprocesses**
  
## <a name="examples"></a>Exemplos  
Este exemplo simples define o valor **context_info** como `0x1256698456` e, em seguida, usa a função `CONTEXT_INFO` para recuperar o valor.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Veja também
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
