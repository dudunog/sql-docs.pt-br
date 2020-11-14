---
description: Criar um rastreamento (Transact-SQL)
title: Criar um rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], example
- traces [SQL Server], creating
ms.assetid: 79dd4254-e3c6-467a-bb6f-f99e51757e99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff2970bf4d450c425f169be7b2bb72c24db7d2d0
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364788"
---
# <a name="create-a-trace-transact-sql"></a>Criar um rastreamento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como usar procedimentos armazenados para criar um rastreamento.  
  
### <a name="to-create-a-trace"></a>Para criar um rastreamento  
  
1.  Execute **sp_trace_create** com os parâmetros exigidos para criar um novo rastreamento. O novo rastreamento estará em um estado parado ( *status* é **0** ).  
  
2.  Execute **sp_trace_setevent** com os parâmetros exigidos para selecionar os eventos e as colunas para rastrear.  
  
3.  Opcionalmente, execute **sp_trace_setfilter** para definir qualquer ou uma combinação de filtros.  

     **sp_trace_setevent** e **sp_trace_setfilter** só podem ser executados em rastreamentos existentes que estejam parados.  
  
    > [!IMPORTANT]  
    >  Ao contrário dos procedimentos armazenados comuns, os parâmetros de todos os procedimentos armazenados do SQL Server Profiler ( <strong>sp_trace_ *xx*</strong>) são estritamente tipados e não são compatíveis com a conversão automática de tipo de dados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="examples"></a>Exemplos

 O código a seguir demonstra a criação de um rastreamento usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ele está em três partes: criação do rastreamento, população do arquivo de rastreamento e interrupção do rastreamento. Personalize o rastreamento adicionando os eventos que deseja rastrear. Para obter a lista de eventos e colunas, veja [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
### <a name="a-create-a-trace"></a>a. Criar um rastreamento
 O seguinte código cria um rastreamento, acrescenta eventos ao rastreamento e depois inicia o rastreamento:  
  
```  
DECLARE @RC int, @TraceID int, @on BIT  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\SampleTrace'  
  
-- Select the return code to see if the trace creation was successful.  
SELECT RC = @RC, TraceID = @TraceID  
  
-- Set the events and data columns you need to capture.  
SELECT @on = 1  
  
-- 10 is RPC:Completed event. 1 is TextData column.   
EXEC sp_trace_setevent @TraceID, 10, 1, @on   
-- 13 is SQL:BatchStarting, 11 is LoginName  
EXEC sp_trace_setevent @TraceID, 13, 11, @on   
-- 13 is SQL:BatchStarting, 14 is StartTime  
EXEC sp_trace_setevent @TraceID, 13, 14, @on   
-- 12 is SQL:BatchCompleted, 15 is EndTime  
EXEC sp_trace_setevent @TraceID, 12, 15, @on   
-- 13 is SQL:BatchStarting, 1 is TextData  
EXEC sp_trace_setevent @TraceID, 13, 1, @on   
  
-- Set any filter. Not provided in this example  
--EXEC sp_trace_setfilter 1, 10, 0, 6, N'%Profiler%'  
  
-- Start Trace (status 1 = start)  
EXEC @RC = sp_trace_setstatus @TraceID, 1  
GO  
  
```  
  
### <a name="b-populate-the-trace-file"></a>B. Popular o arquivo de rastreamento
 Agora que o rastreamento foi criado e iniciado, execute o código a seguir para popular o rastreamento com atividade.  
  
```  
SELECT * FROM master.sys.databases  
GO  
SELECT * FROM ::fn_trace_getinfo(default)  
GO  
  
```  
  
### <a name="c-stop-the-trace"></a>C. Parar o rastreamento
 O rastreamento pode ser interrompido e reiniciado a qualquer momento. Neste exemplo, execute o código a seguir para interromper o rastreamento, fechar o rastreamento e excluir sua definição.  
  
```  
DECLARE @TraceID int  
-- Populate a variable with the trace_id of the current trace  
SELECT  @TraceID = TraceID FROM ::fn_trace_getinfo(default) WHERE VALUE = N'C:\SampleTrace.trc'  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2  
  
```  
  
### <a name="d-examine-the-trace-file"></a>D. Examinar o arquivo de rastreamento
 Para examinar o arquivo de rastreamento, abra o arquivo SampleTrace.trc usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)  
  
  
