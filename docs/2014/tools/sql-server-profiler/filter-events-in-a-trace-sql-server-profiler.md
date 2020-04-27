---
title: Filtrar eventos em um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 0fd63573-3b35-4f67-9e1e-ed9aabee11a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 851fd1c1f3249a36af6de66aaa374088fab1c1ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63298165"
---
# <a name="filter-events-in-a-trace-sql-server-profiler"></a>Filtrar eventos em um rastreamento (SQL Server Profiler)
  Os filtros limitam os eventos coletados em um rastreamento. Se não houver um filtro definido, serão retornados todos os eventos das classes de evento selecionadas na saída do rastreamento. Não é obrigatório definir um filtro para um rastreamento. Porém, um filtro minimiza a sobrecarga incorrida durante o rastreamento.  
  
 Os filtros são adicionados às definições de rastreamento por meio da guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** ou **Propriedades do Modelo de Rastreamento** .  
  
### <a name="to-filter-events-in-a-trace"></a>Para filtrar eventos em um rastreamento  
  
1.  Na caixa de diálogo **Propriedades do Rastreamento** ou **Propriedades do Modelo de Rastreamento** , clique na guia **Seleção de Eventos** .  
  
     A guia **Seleção de Eventos** contém um controle de grade. O controle de grade é uma tabela que contém cada uma das classes de evento rastreáveis. A tabela contém uma linha para cada classe de evento. As classes de evento podem diferir ligeiramente, dependendo do tipo e versão de servidor com o qual você está conectado. As classes de evento são identificadas na coluna **Events**da grade e são agrupadas por categoria de evento. As colunas restantes listam as colunas de dados que podem ser retornadas para cada classe de evento.  
  
2.  Clique em **Filtros de Coluna.**  
  
     A caixa de diálogo **Editar Filtro**é exibida. A caixa de diálogo **Editar Filtro**contém uma lista de operadores de comparação que podem ser usados para filtrar eventos em um rastreamento.  
  
3.  Para aplicar um filtro, clique no operador de comparação e digite um valor a usar para o filtro.  
  
4.  Clique em **OK**.  
  
 **Considerações:**  
  
-   Se definir condições de filtro nas colunas de dados **StartTime** e **EndTime** da guia Seleção de Eventos, verifique se:  
  
    -   A data inserida corresponda a este formato: `YYYY/MM/DD HH:mm:sec`.  
  
         -OU-  
  
    -   **Usar configurações regionais para exibir valores de data e hora** está marcado na caixa de diálogo **Opções Gerais** . Para exibir a caixa de diálogo **Opções Gerais**, no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Ferramentas**, clique em **Opção**.  
  
         -E-  
  
    -   A data inserida esteja entre 1° de janeiro de 1753 e 31 de dezembro de 9999.  
  
-   Se rastrear eventos do utilitário **osql** ou do utilitário **sqlcmd** , sempre acrescente **%** aos filtros na coluna de dados **TextData** .  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
