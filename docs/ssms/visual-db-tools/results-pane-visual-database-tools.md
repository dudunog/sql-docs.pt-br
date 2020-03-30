---
title: Painel de Resultados
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: b6c7817fd90085ab4a7520cb98481dabea3b9558
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255205"
---
# <a name="results-pane-visual-database-tools"></a>Painel de Resultados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O painel Resultados mostra os resultados da consulta SELECT executada mais recentemente. (Os resultados de outros tipos de consultas são exibidos em caixas de mensagens.) Para abrir o painel Resultados, abra ou crie uma consulta ou exibição ou retorne os dados de uma tabela. Se o painel Resultados não for exibido por padrão, no menu **Designer de Consulta** , aponte para **Painel**e clique em **Resultados**.  
  
## <a name="what-you-can-do-in-the-results-pane"></a>O que você pode fazer no painel Resultados  
  
-   Exibir o conjunto de resultados para a consulta SELECT executada mais recentemente em uma grade tipo planilha.  
  
-   Você pode editar os valores em colunas individuais no conjunto de resultados, adicionar linhas novas e excluir linhas existentes para consultas ou exibições que mostram dados de uma única tabela ou exibição.  
  
## <a name="limitations-in-the-results-pane"></a>Limitações do painel Resultados  
  
-   Em alguns casos, somente os resultados retornados por funções com valor de tabela podem ser atualizados.  
  
-   As consultas ou as exibições que incluem colunas de mais de uma tabela ou exibição não podem ser atualizadas.  
  
-   Os resultados retornados por um procedimento armazenado não podem ser atualizados.  
  
-   As consultas ou as exibições que utilizam cláusulas GROUP BY ou DISTINCT não podem ser atualizadas.  
  
## <a name="navigating-in-the-results-pane"></a>Navegando no painel Resultados  
Você pode navegar rapidamente pelos registros, utilizando a barra de navegação da parte inferior do painel Resultados.  
  
Há botões para seguir até o primeiro e o último registro, registros anteriores e posteriores, e para seguir até determinado registro.  
  
Para ir até um registro específico, digite o número da linha na caixa de texto da barra de navegação e pressione ENTER.  
  
Para obter informações sobre como usar atalhos de teclado no Designer de Consulta e Exibição, veja [Navegar no Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Mantendo o conjunto de resultados sincronizado com a definição de consulta  
Enquanto se está trabalhando nos resultados de uma consulta ou exibição, é possível que os registros do painel de resultados percam a sincronização com a definição da consulta. Por exemplo, se você executar uma consulta para quatro entre cinco colunas de uma tabela e, depois, utilizar o painel Diagrama para adicionar a quinta coluna à definição da consulta, os dados da quinta coluna não serão adicionados automaticamente ao painel Resultados. Para fazer com que o painel de resultados reflita a nova definição de consulta, execute novamente a consulta.  
  
Se a consulta for alterada, será exibido um ícone de alerta e o texto “Consulta alterada” no canto inferior direito do painel Resultados. O ícone será repetido no canto superior esquerdo do painel.  
  
## <a name="see-also"></a>Consulte Também  
[Criar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Executar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Painel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Trabalhar com dados no painel de resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
