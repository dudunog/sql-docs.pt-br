---
title: Propriedades do modelo de rastreamento (guia Seleção de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f70460e68d1161fa8aa718a5e5264a8e6f0782df
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928161"
---
# <a name="trace-template-properties-events-selection-tab"></a>Propriedades do Modelo de Rastreamento (guia Seleção de Eventos)
  Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Modelo de Rastreamento** para exibir, editar ou especificar classes de evento e colunas de dados para incluir um modelo de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] .  
  
## <a name="options"></a>Opções  
 Coluna**Eventos**  
 Especifique os eventos que devem ser rastreados selecionando ou desmarcando a caixa de seleção na coluna Eventos. Os eventos são organizados por categoria de evento.  
  
 Se você selecionou **Basear novo modelo no existente** na guia **Geral** , os eventos serão selecionados automaticamente de acordo com o modelo especificado. Para obter mais informações sobre classes de evento, consulte [Referência de classe de evento do SQL Server](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Colunas de dados  
 Especifique as colunas de dados que devem ser rastreadas marcando a caixa que corresponde ao evento e a coluna de dados que você precisa. Todas as colunas de evento pertinentes serão selecionadas por padrão para cada evento incluído no rastreamento, se a caixa de seleção correspondente ao evento estiver marcada. Se você selecionou **Basear novo modelo no existente** na guia **Geral** , as colunas de dados e os filtros serão selecionados automaticamente de acordo com o modelo especificado.  
  
 Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
  
 **Mostrar todos os eventos**  
 Mostra todos os eventos disponíveis. Essa opção será selecionada por padrão se você estiver criando um novo modelo que não seja baseado em um modelo existente. Desmarque para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** .  
  
 **Mostrar todas as colunas**  
 Mostra todas as colunas de dados disponíveis. Essa opção será selecionada por padrão se você estiver criando um novo modelo que não seja baseado em um modelo existente. Desmarque para ocultar todas as colunas de dados não selecionadas na guia **Seleção de Eventos** .  
  
 **Filtros de coluna**  
 Inicia a caixa de diálogo **Editar Filtro**, que exibe um ícone de filtro à esquerda do rótulo da coluna de dados. Use a caixa de diálogo **Editar Filtro** para editar filtros de coluna de dados.  
  
 **Organizar colunas**  
 Altera a ordem das colunas no rastreamento e agrupa os resultados em uma ou mais colunas.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Organizar colunas exibidas em um &#40;de rastreamento SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Filtrar eventos em um &#40;de rastreamento SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Exibir informações de filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificar um filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
