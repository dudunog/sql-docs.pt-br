---
title: Criar aliases de coluna
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: ecf5cbcac382bc088c5a04595d554e4d8ea124ba
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254356"
---
# <a name="create-column-aliases-visual-database-tools"></a>Criar aliases de coluna (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar aliases para nomes de coluna para tornar mais fácil o trabalho com nomes de colunas, cálculos e valores de resumo. Por exemplo, você pode criar um alias de coluna para:  
  
-   Criar um nome de coluna, tal como "Total Amount", para uma expressão como `(quantity * unit_price)` ou para uma função de agregação.  
  
-   Criar um formulário resumido de um nome de coluna, como `"d_id"` para `"discounts.stor_id."`  
  
Após ter definido um alias de coluna, você pode usar o alias em uma consulta Select para especificar a saída de consulta.  
  
### <a name="to-create-a-column-alias"></a>Para criar um alias de coluna  
  
1.  No **Painel de Critérios**, localize a linha contendo a coluna de dados para a qual você quer criar um alias e, caso necessário, marque-a para saída. Se a coluna de dados já não estiver na grade, acrescente-a.  
  
2.  Na coluna **Alias** para aquela linha, insira o alias. O alias deve seguir todas as convenções de nomenclatura SQL. Se o nome de alias que você entrar contiver espaços, o Designer de Consulta e Visualização coloca delimitadores automaticamente ao redor dele.  
  
## <a name="see-also"></a>Consulte Também  
[Adicionar colunas a consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
