---
title: Destino do contador de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- synchronous event counter target [SQL Server extended events]
- targets [SQL Server extended events], synchronous event counter target
ms.assetid: 342e08d1-dcca-4a71-ae64-cb61b55b85bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddf153da7af2906fe7167c8cb2b77d9100d1154f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064914"
---
# <a name="event-counter-target"></a>Destino de contador de eventos
  O destino do contador de eventos conta todos os eventos ocorridos durante uma sessão de Eventos Estendidos. Com o uso do destino do contador de eventos, é possível obter informações sobre as características da carga de trabalho, sem adicionar a sobrecarga da coleção de eventos. Esse destino não tem nenhum parâmetro personalizável.  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino do contador de eventos a uma sessão de Eventos Estendidos, você deve incluir a instrução a seguir ao criar ou alterar uma sessão de evento:  
  
```  
ADD TARGET package0.event_counter  
```  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 Para examinar a saída do destino do contador de eventos, você pode usar a consulta a seguir, substituindo *session_name* pelo nome da sessão de evento:  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 O exemplo a seguir mostra o formato da saída de destino do contador de eventos.  
  
```  
<CounterTarget truncated = "0">  
  <Packages>  
    <Package name = "[package name]">  
      <Event name = "[event name]" count = "[number]" />  
    </Package>  
  </Packages>  
</CounterTarget>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server destinos de eventos estendidos](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys. dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CRIAR sessão de evento &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
