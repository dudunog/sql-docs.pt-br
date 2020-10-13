---
title: Monitorar a atividade do sistema usando Eventos Estendidos
description: Use os Eventos Estendidos com o Rastreamento de Eventos para Windows para monitorar a atividade do sistema. Saiba como usar CREATE EVENT SESSION, ALTER EVENT SESSION e DROP EVENT SESSION.
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c0c573d3271346e8e42fa0fb1a06fba0b20a136
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866782"
---
# <a name="monitor-system-activity-using-extended-events"></a>Monitorar a atividade do sistema usando Eventos Estendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este procedimento ilustra como os Eventos Estendidos podem ser usados com o Rastreamento de Eventos do Windows (ETW) para monitorar a atividade do sistema. O procedimento também mostra como são usadas as instruções CREATE EVENT SESSION, ALTER EVENT SESSION e DROP EVENT SESSION.  
  
 A realização dessas tarefas envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para aplicar o procedimento a seguir. O procedimento também requer o uso do prompt de comando para executar comandos ETW.  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>Para monitorar a atividade do sistema usando Eventos Estendidos  
  
1.  No Editor de Consultas, emita as instruções a seguir para criar uma sessão de eventos e adicionar dois eventos. Esses eventos, checkpoint_begin e checkpoint_end, são acionados no início e no final de um ponto de verificação de banco de dados.  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  Adicione o destino da segmentação com 32 segmentos, para contar o número de pontos de verificação com base na ID de banco de dados.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  Emita as instruções a seguir para adicionar o destino do ETW. Isso lhe permitirá examinar os eventos de início e fim, utilizados para determinar a duração do ponto de verificação.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  Emita as instruções a seguir para iniciar a sessão e começar a coleta de eventos.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  Emita as instruções a seguir para provocar o acionamento de três eventos.  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  Emita as instruções a seguir para exibir as contagens dos eventos.  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  No prompt de comando, emita os comandos a seguir para exibir os dados do ETW.  
  
    > [!NOTE]  
    >  Para obter ajuda sobre o comando **tracerpt** , no prompt de comando, digite `tracerpt /?`.  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  Emita as instruções a seguir para parar a sessão de eventos e removê-la do servidor.  

    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Exibições de catálogo de eventos estendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Destinos de eventos estendidos do SQL Server](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))  
  
