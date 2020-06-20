---
title: Pesquisar um documento ativo de forma incremental
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: rothja
ms.author: jroth
ms.openlocfilehash: a7c378345848edf8c3a4de8c6d8d6c50ce101389
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85009357"
---
# <a name="search-an-active-document-incrementally"></a>Pesquisar um documento ativo de forma incremental
  É possível pesquisar um único documento ou janela de forma incremental digitando texto. A operação de pesquisa realça o primeiro conjunto de caracteres que corresponde aos caracteres digitados durante a pesquisa incremental no documento ou na janela. A pesquisa incremental pesquisa automaticamente todo o texto dentro de um documento ou de uma janela, com exceção de texto oculto.  
  
 Na opção **Diferenciar Maiúsculas de Minúsculas** , a pesquisa incremental usa os critérios de sua pesquisa anterior. Por exemplo, se você pesquisou vários arquivos usando a caixa de diálogo **Localizar nos Arquivos** e selecionou **Distinguir Maiúsculas de Minúsculas**, se uma nova pesquisa for incremental, a pesquisa considerará maiúsculas e minúsculas.  
  
### <a name="to-search-incrementally"></a>Para pesquisar incrementalmente  
  
1.  Abra o arquivo ou a janela que você deseja pesquisar.  
  
2.  No menu **Editar** , aponte para **Avançado**e clique em **Pesquisa Incremental**.  
  
     O ícone de cursor muda para um binóculo com uma seta, indicando a direção de pesquisa e a barra de status exibe "Pesquisa Incremental".  
  
3.  Comece a digitar a cadeia de caracteres de texto.  
  
     A barra de status exibe o texto que você está digitando, enquanto o editor realça a primeira ocorrência que corresponde ao texto. Enquanto você continua a digitação, o editor se move para a próxima correspondência e a destaca. Se não houver correspondências disponíveis, a barra de status exibirá o seguinte:  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 As pesquisas incrementais são executadas no local atual, para baixo e da esquerda para a direita no documento. As pesquisas incrementais podem ser feitas usando teclas de atalho do teclado.  
  
> [!NOTE]  
>  Para obter uma lista completa de teclas de atalho do teclado, consulte [Atalhos de teclado do SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisar e substituir](search-and-replace.md)   
 [Pesquisar documentos interativamente](search-documents-interactively.md)   
 [Pesquisar documentos usando listas de resultados](search-documents-using-results-lists.md)   
 [Pesquisar texto com curingas](search-text-with-wildcards.md)   
 [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md)  
  
  
