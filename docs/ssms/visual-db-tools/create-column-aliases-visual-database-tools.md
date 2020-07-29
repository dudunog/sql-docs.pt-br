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
ms.reviewer: ''
ms.openlocfilehash: c4feb18b5f01b1e999ecec5b5b8e022230912d8f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85977803"
---
# <a name="create-column-aliases-visual-database-tools"></a>Criar aliases de coluna (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
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
  
