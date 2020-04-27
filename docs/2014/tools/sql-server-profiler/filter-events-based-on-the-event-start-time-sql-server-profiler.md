---
title: Filtrar eventos com base na hora de término do evento (SQL Server Profiler) | Microsoft Docs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event start times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0cd08ce16341022072c76fc1bf073d1a469d9273
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63192908"
---
# <a name="filter-events-based-on-the-event-start-time-sql-server-profiler"></a>Filtrar eventos com base na hora de início do evento (SQL Server Profiler)
  Este tópico descreve como filtrar eventos de rastreamento de acordo com a hora de início do evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-an-event-based-on-the-event-start-time"></a>Para filtrar eventos com base na hora de início do evento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se a opção **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver marcada, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista de nomes **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um destino para os resultados do rastreamento.  
  
5.  Na guia **Seleção de Eventos**, clique no título de coluna **StartTime** . Você também pode clicar com o botão direito do mouse no título de coluna e clicar em **Editar Filtro de Coluna** para iniciar a caixa de diálogo **Editar Filtro** .  
  
6.  Expanda **maior que** ou **menor que**e insira um `datetime` valor no campo que aparece abaixo do operador de comparação.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
