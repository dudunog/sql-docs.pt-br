---
description: Especificar várias condições de pesquisa para diversas colunas (Visual Database Tools)
title: Especificar várias condições de pesquisa para diversas colunas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 5a5f5d4e3396e3ccbff7280fbae14036015ba5eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445969"
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>Especificar várias condições de pesquisa para diversas colunas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode expandir ou estreitar o escopo de sua consulta incluindo várias colunas de dados como parte de seu critério de pesquisa. Por exemplo, você pode querer:  
  
-   Pesquisar funcionários que já trabalham há mais de cinco anos na empresa ou que possuam determinados cargos.  
  
-   Pesquisar um livro publicado por um editor específico e que pertence ao setor de culinária.  
  
Para criar uma consulta que pesquisa valores em duas (ou mais) colunas, você especifica uma condição OR. Para criar uma consulta que atenda todas as condições em duas (ou mais) colunas, você especifica uma condição AND.  
  
## <a name="specifying-an-or-condition"></a>Especificando um critério OR  
Para criar várias condições vinculadas a OR, você coloca cada condição separada em uma coluna diferente do painel Critérios.  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>Para especificar uma condição OR para duas colunas diferentes  
  
1.  No [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), adicione as colunas a serem pesquisadas.  
  
2.  Na coluna **Filtro** da primeira coluna a ser pesquisada, especifique a primeira condição.  
  
3.  Na coluna **Ou...** da segunda coluna de dados a ser pesquisada, especifique a segunda condição, deixando a coluna **Filtro** em branco.  
  
    O Designer de Consulta e Exibição cria uma cláusula WHERE que contém um critério OR, como o seguinte:  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja adicionar. Utilize uma coluna **Ou...** diferente para cada condição nova.  
  
## <a name="specifying-an-and-condition"></a>Especificando um critério AND  
Para pesquisar várias colunas de dados usando condições vinculadas a AND, coloque todas as condições na coluna **Filtro** da grade.  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>Para especificar uma condição AND para duas colunas diferentes  
  
1.  No [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), adicione as colunas a serem pesquisadas.  
  
2.  Na coluna **Filtro** da primeira coluna de dados a ser pesquisada, especifique a primeira condição.  
  
3.  Na coluna **Filtro** da segunda coluna de dados, especifique a segunda condição.  
  
    O Designer de Consulta e Exibição cria uma cláusula WHERE que contém uma condição AND, igual a:  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  Repita as etapas 2 e 3 para cada condição adicional que você deseja adicionar.  
  
## <a name="see-also"></a>Consulte Também  
[Combinar condições quando AND tiver precedência](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[Combinar condições quando OR tem precedência](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Convenções para combinar condições de pesquisa no painel Critérios](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Especificar critérios de pesquisa](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
