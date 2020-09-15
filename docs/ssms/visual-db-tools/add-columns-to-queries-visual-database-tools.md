---
description: Adicionar colunas a consultas (Visual Database Tools)
title: Adicionar Colunas a Consultas
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 9160ceb8b3fab33e7cc8c8068c418f4c2013bb79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88370102"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Adicionar colunas a consultas (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Para usar uma coluna em uma consulta, você deve adicioná-la à consulta. Você pode adicionar uma coluna para exibi-la na saída da consulta, usá-la para ordenar, pesquisar os conteúdos da coluna, ou para resumir seus conteúdos. Você pode decidir qual das colunas usadas na consulta será incluída no painel de resultados quando a consulta for executada. Para obter mais informações, veja [Remover colunas de resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Para exibir o tipo de dados de uma coluna no Designer de Consulta e Exibição, selecione a tabela ou objeto avaliado pela tabela no **Painel de Diagrama** e na janela de propriedades clique em Lista de Colunas. Em seguida, clique nas **reticências (...)** para abrir a caixa de diálogo **Lista de Colunas**.  
  
Sempre que você usar uma coluna em uma consulta, você pode também usar uma expressão que consiste em qualquer combinação de colunas, literais, operadores e funções.  
  
### <a name="to-add-an-individual-column"></a>Para adicionar uma coluna individual  
  
-   No **Painel de Diagrama**, marque a caixa de seleção próxima à coluna que você quer incluir.  
  
    - ou -  
  
-   No **Painel Critérios**, mova para a primeira linha de grade em branco, clique no campo da coluna **Coluna** e selecione um nome de coluna na lista suspensa.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Para adicionar todas as colunas de uma tabela ou objeto avaliado por tabela  
  
-   No **Painel de Diagrama**, marque a caixa de seleção ao lado de **#42;(Todas as Colunas)** .  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Para adicionar todas as colunas para todas as tabelas e objetos estruturados por tabela  
  
1.  Verifique se nenhuma linha de junção está selecionada no **Painel de Operações de Tabela** .  
  
2.  Clique com o botão direito do mouse no espaço em branco da janela Design e escolha **Propriedades** no menu de atalho.  
  
3.  Na janela Propriedades, clique em **Todas as colunas de saída** e escolha **Sim** ou **Não** na lista suspensa.  
  
## <a name="see-also"></a>Consulte Também  
[Remover colunas de resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Remover colunas de consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
