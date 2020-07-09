---
title: Eventos estendidos equivalentes às classes de rastreamento de eventos do SQL
description: Este artigo mostra como ver as ações e os eventos dos Eventos Estendidos que são equivalentes a cada evento de Rastreamento do SQL e suas colunas associadas.
ms.date: 03/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1275488eeed0aaccf284490fafd0a3a83bab7aff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756785"
---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>Exibir os Eventos Estendidos equivalentes às classes de evento de Rastreamento do SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sql-asdb.md)]

  Se você desejar usar os Eventos Estendidos para coletar dados de evento equivalentes a colunas e classes de evento do Rastreamento do SQL, será útil entender como os eventos do Rastreamento do SQL são mapeados para os eventos e as ações dos Eventos Estendidos.  
  
 Você pode usar o seguinte procedimento para exibir os eventos e as ações dos Eventos Estendidos que são equivalentes a cada evento do Rastreamento do SQL e suas colunas associadas.  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>Para exibir os equivalentes de Eventos Estendidos a eventos do Rastreamento do SQL usando o Editor de Consulta

- No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute a seguinte consulta:

   ```sql
   USE MASTER;
   GO
   SELECT DISTINCT
      tb.trace_event_id,
      te.name            AS 'Event Class',
      em.package_name    AS 'Package',
      em.xe_event_name   AS 'XEvent Name',
      tb.trace_column_id,
      tc.name            AS 'SQL Trace Column',
      am.xe_action_name  AS 'Extended Events action'
   FROM
                sys.trace_events         te
      LEFT JOIN sys.trace_xe_event_map   em ON te.trace_event_id  = em.trace_event_id
      LEFT JOIN sys.trace_event_bindings tb ON em.trace_event_id  = tb.trace_event_id
      LEFT JOIN sys.trace_columns        tc ON tb.trace_column_id = tc.trace_column_id
      LEFT JOIN sys.trace_xe_action_map  am ON tc.trace_column_id = am.trace_column_id
   ORDER BY te.name, tc.name
   ```

Ao exibir os resultados, observe o seguinte:  

- Se todas as colunas retornarem NULL com exceção da coluna Event Class, isso indicará que a classe de evento não foi migrada do Rastreamento do SQL.  
  
-   Se apenas o valor da coluna Extended Events for NULL, isso indicará que qualquer um das seguintes condições é verdadeira:  
  
    -   A coluna Rastreamento do SQL é mapeada para um dos campos de dados associados ao evento de Eventos Estendidos.  
  
        > [!NOTE]  
        > Cada evento dos Eventos Estendidos tem um conjunto padrão de campos de dados que são incluídos automaticamente no conjunto de resultados.  
  
    -   A coluna de ação não tem um equivalente significativo dos Eventos Estendidos. Um exemplo disso é a coluna EventClass no Rastreamento do SQL. Essa coluna não é necessária nos Eventos Estendidos porque o nome do evento atende ao mesmo objetivo.  
  
-   Para as classes de evento do Rastreamento do SQL configuráveis pelo usuário (UserConfigurable:1 a UserConfigurable:9), os Eventos Estendidos usam um único evento para substituí-las. O evento é chamado user_event. Este evento é gerado por meio de sp_trace_generateevent, o mesmo procedimento armazenado usado pelo Rastreamento do SQL. O evento user_event é retornado, independentemente de qual ID de evento é passada para o procedimento armazenado. No entanto, um campo event_id é retornado como parte dos dados do evento. Isso permite a você criar um predicado baseado na ID do evento. Por exemplo, se você usar UserConfigurable:0 (ID de evento = 82) no código, poderá adicionar o evento user_event à sessão e especificar o predicado “event_id = 82”. Portanto, você não precisa alterar o código, pois o procedimento armazenado sp_trace_generateevent gera o evento user_event dos Eventos Estendidos, e a classe de evento equivalente do Rastreamento do SQL.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)  
  
  
