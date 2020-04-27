---
title: Organizar as colunas exibidas em um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- organizing trace columns displayed [SQL Server]
- arranging trace columns displayed
- traces [SQL Server], data columns
ms.assetid: 6b923f94-0eb1-467e-82f6-ceed43f77017
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1a884f7c45accefb248029d148feb8b521e6ff4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63240542"
---
# <a name="organize-columns-displayed-in-a-trace-sql-server-profiler"></a>Organizar colunas exibidas em um rastreamento (SQL Server Profiler)
  É possível agrupar as colunas de dados em um rastreamento selecionando **Organizar Colunas** na tabela de rastreamento ou na caixa de diálogo **Propriedades do Arquivo de Rastreamento** , ou durante a definição do rastreamento. Agrupar as colunas de dados permite-lhe analisar melhor a saída de rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Para obter mais informações, veja [Exibir e analisar rastreamentos com o SQL Server Profiler](view-and-analyze-traces-with-sql-server-profiler.md).  
  
 **Organizar Colunas** permite agrupar os eventos do rastreamento ou agrupá-los e agregá-los pelas colunas de dados que você selecionar.  
  
-   Escolha várias colunas de dados para agrupar apenas eventos de rastreamento. Quando várias colunas de dados são selecionadas para o agrupamento, a janela de rastreamento exibe os eventos agrupados pelos valores nas colunas de dados escolhidas. O exemplo a seguir mostra como a grade da janela de rastreamento apareceria se você selecionasse as colunas **Duration** e **StartTime** para agrupamento. Observe que os valores da coluna **Duration** são exibidos em ordem crescente, seguidos dos valores de **StartTime** .  
  
|Duration|StartTime|EventClass|ClientProcessID|  
|--------------|---------------|----------------|---------------------|  
||12/12/2006 3:16:43 PM|SQL:StmtStarting|2124|  
|0|12/12/2006 5:39:23 PM|Auditar logon|648|  
|1|12/12/2006 5:24:44 PM|SQL:StmtStarting|2124|  
|25|12/12/2006 5:24:44 PM|SQL:StmtCompleted|648|  
  
-   Selecione apenas uma coluna para agrupar e agregar os eventos do rastreamento. Quando uma única coluna de dados é selecionada para o agrupamento, a janela de rastreamento exibe os eventos agrupados pelos valores nessa coluna de dados e recolhe todos os eventos debaixo dela. Um sinal de adição ( **+** ) aparece à esquerda do evento na coluna de dados selecionada para o agrupamento com o número de eventos recolhidos sob ela entre parênteses, à direita do evento. O exemplo a seguir mostra como a grade da janela de rastreamento apareceria se você selecionasse apenas a coluna **EventClass** para agrupamento. Observe que todos os eventos estão organizados sob a coluna de dados **EventClass** . Para visualizar todos os eventos, clique no sinal mais para expandir e exibir todas as classes de evento daquele tipo.  
  
|EventClass|StartTime|Duration|ClientProcessID|  
|----------------|---------------|--------------|---------------------|  
|+ ExistingConnection (6)||||  
|+ SQL:BatchStarting (25)||||  
|+ SQL:StmtCompleted (11)||||  
|+ SQL:SmtStarting (21)||||  
  
### <a name="to-group-data-columns-displayed-in-a-trace"></a>Para agrupar as colunas de dados exibidas em um rastreamento  
  
1.  Abra um arquivo ou tabela de rastreamento existente.  
  
2.  No menu **Arquivo** , clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Arquivo de Rastreamento** ou **Propriedades da Tabela de Rastreamento** , clique na guia **Seleção de Eventos** .  
  
4.  Na guia **Seleção de Eventos** , clique em **Organizar Colunas**.  
  
5.  Na caixa de diálogo **Organizar Colunas** , selecione as colunas que deseja exibir no grupo e clique em **Para Cima** para movê-las para baixo de **Grupos**. Tendo movido todas as colunas que deseja para baixo de **Grupos**, você pode usar os botões **Para Cima** e **Para Baixo** para reordená-las.  
  
     Mover os nomes das colunas de dados para a lista **Grupos** significa que o rastreamento exibido será primeiro organizado na ordem em que as colunas de dados aparecem na lista **Grupos** , depois pela segunda coluna de dados na lista **Grupos** e assim por diante.  
  
6.  Clique em **OK** na caixa de diálogo **Organizar Colunas** e, em seguida, clique em **OK** na caixa de diálogo **Propriedades da Tabela de Rastreamento** ou **Propriedades do Arquivo de Rastreamento** .  
  
     Depois do clique em **OK** na caixa de diálogo **Propriedades da Tabela de Rastreamento** ou **Propriedades do Arquivo de Rastreamento** , as colunas de dados são reorganizadas no rastreamento exibido. A coluna de dados que você moveu para a primeira posição na lista **Grupos** aparece primeiro na exibição do rastreamento, quando se lê a grade da esquerda para a direita. As linhas no rastreamento são organizadas, em ordem crescente, pelos valores contidos nas colunas de dados incluídas na lista **Grupos** . As colunas escolhidas para o agrupamento permanecem fixas na exibição, mas é possível rolar para a direita ou para a esquerda e visualizar as outras colunas.  
  
7.  Para desagrupar os dados do rastreamento exibido, clique em **Exibição Agrupada** no menu **Exibir** para cancelar a seleção. Se desejar voltar à exibição agrupada, clique outra vez em **Exibição Agrupada** no menu **Exibir** para selecioná-la novamente.  
  
### <a name="to-group-and-aggregate-data-columns-in-a-trace"></a>Para agrupar e agregar as colunas de dados em um rastreamento  
  
1.  Abra um arquivo ou tabela de rastreamento existente.  
  
2.  No menu **Arquivo** , clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Arquivo de Rastreamento** ou **Propriedades da Tabela de Rastreamento** , clique na guia **Seleção de Eventos** .  
  
4.  Na guia **Seleção de Eventos** , clique em **Organizar Colunas**.  
  
5.  Na caixa de diálogo **Organizar Colunas** , selecione a coluna pela qual deseja agrupar e agregar os eventos do rastreamento exibido. Clique **Para cima** para mover o nome de coluna sob **Grupos**. Você pode usar os botões **Para Cima** e **Para Baixo** para reorganizar as colunas restantes em **Colunas** , se necessário.  
  
6.  Clique em **OK** na caixa de diálogo **Organizar Colunas** e, em seguida, clique em **OK** na caixa de diálogo **Propriedades da Tabela de Rastreamento** ou **Propriedades do Arquivo de Rastreamento** .  
  
     Depois do clique em **OK** na caixa de diálogo **Propriedades da Tabela de Rastreamento** ou **Propriedades do Arquivo de Rastreamento** , as colunas de dados são reorganizadas no rastreamento exibido. Todos os outros eventos de coluna de dados são agregados sob a coluna de dados que você moveu para a lista **Grupos** . Clique no sinal de adição ( **+** ), à esquerda do evento na coluna de dados selecionada para a agregação, para expandi-la e ver todos os eventos daquele tipo. A coluna escolhida para a agregação permanece fixa na exibição, mas é possível rolar para a direita ou para a esquerda e visualizar as outras colunas.  
  
7.  Para voltar à exibição normal dos dados do rastreamento, clique em **Exibição Agregada** no menu **Exibir** para cancelar a seleção. Se desejar voltar à exibição agregada, clique outra vez em **Exibição Agregada** no menu **Exibir** para selecioná-la novamente. Note que você também pode clicar em **Exibição Agrupada** no menu **Exibir** para exibir os eventos do rastreamento agrupado sem que eles sejam recolhidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)   
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)   
 [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)  
  
  
