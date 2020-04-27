---
title: Criar aliases de coluna (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a6be65da2da5da5c025520314c069258aeb7bfb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184356"
---
# <a name="create-column-aliases-visual-database-tools"></a>Criar aliases de coluna (Visual Database Tools)
  Você pode criar aliases para nomes de coluna para tornar mais fácil o trabalho com nomes de colunas, cálculos e valores de resumo. Por exemplo, você pode criar um alias de coluna para:  
  
-   Criar um nome de coluna, tal como "Total Amount", para uma expressão como `(quantity * unit_price)` ou para uma função de agregação.  
  
-   Criar um formulário resumido de um nome de coluna, como `"d_id"` para `"discounts.stor_id."`  
  
 Após ter definido um alias de coluna, você pode usar o alias em uma consulta Select para especificar a saída de consulta.  
  
### <a name="to-create-a-column-alias"></a>Para criar um alias de coluna  
  
1.  No **Painel de Critérios**, localize a linha contendo a coluna de dados para a qual você quer criar um alias e, caso necessário, marque-a para saída. Se a coluna de dados já não estiver na grade, acrescente-a.  
  
2.  Na coluna **Alias** para aquela linha, insira o alias. O alias deve seguir todas as convenções de nomenclatura SQL. Se o nome de alias que você entrar contiver espaços, o Designer de Consulta e Visualização coloca delimitadores automaticamente ao redor dele.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar colunas a consultas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Classificar e agrupar resultados de consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Resumir os resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
