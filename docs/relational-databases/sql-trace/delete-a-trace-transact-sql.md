---
description: Excluir um rastreamento (Transact-SQL)
title: Excluir um rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d3264c9fe9622bdddee3aecd002193c245c5b457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455352"
---
# <a name="delete-a-trace-transact-sql"></a>Excluir um rastreamento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como usar procedimentos armazenados para excluir um rastreamento.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Para excluir um rastreamento  
  
1.  Execute **sp_trace_setstatus** especificando `@status = 0` para interromper o rastreamento.  
  
2.  Execute **sp_trace_setstatus** especificando `@status = 2` para encerrar o rastreamento e excluir suas informações do servidor.  
  
> [!NOTE]  
>  Um rastreamento deve ser interrompido primeiro antes de ser encerrado.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
