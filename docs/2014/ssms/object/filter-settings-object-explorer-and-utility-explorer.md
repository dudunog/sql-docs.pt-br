---
title: Configurações de Filtro (Pesquisador de Objetos e Gerenciador do Utilitário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.filtersettings.f1
- sql12.swb.common.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd040bbf0f6e3f5e150d45df41ea676a71c6e03a
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859218"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Configurações de Filtro (Pesquisador de Objetos e Gerenciador do Utilitário)
  Use essa caixa de diálogo para especificar um filtro. Um filtro permite que você configure o Pesquisador de Objetos e o Gerenciador do Utilitário para exibir apenas os itens que atendam aos critérios específicos. Por exemplo, você pode usar um filtro para mostrar apenas os trabalhos com nomes que contêm a palavra "Manutenção". O cabeçalho da caixa de diálogo **Configurações de Filtro** contém o nome do servidor e pode conter o nome do banco de dados.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Propriedade**  
 Exibe a propriedade a ser filtrada.  
  
 **Operador**  
 Seleciona o modo que o filtro aplica o valor à propriedade. Existem as seguintes opções:  
  
-   **Igual a**  
  
     O filtro mostra os itens onde a propriedade e o valor têm uma correspondência exata.  
  
-   **Contém**  
  
     O filtro mostra os itens onde a propriedade contém o valor. A propriedade pode conter outro texto.  
  
-   **Não contém**  
  
     O filtro mostra os itens onde a propriedade não contém o valor.  
  
-   **Menor que**  
  
     Disponível para datas, esse filtro mostra os itens cuja data está antes do valor fornecido.  
  
-   **Menor ou igual a**  
  
     Disponível para datas, esse filtro mostra os itens cuja data contém ou está antes do valor fornecido.  
  
-   **Maior que**  
  
     Disponível para datas, esse filtro mostra os itens cuja data está depois do valor fornecido.  
  
-   **Maior ou igual a**  
  
     Disponível para datas, esse filtro mostra os itens cuja data contém ou está depois do valor fornecido.  
  
-   **Entre**  
  
     Disponível para datas, este filtro mostra os itens cuja data está entre duas datas fornecidas. Selecione **Entre** e pressione TAB para adicionar outra linha permitindo a entrada da segunda data.  
  
-   **Não entre**  
  
     Disponível para datas, esse filtro mostra os itens cuja data está antes ou depois das duas datas fornecidas. Selecione **Não entre** e saia da coluna **Operador** para adicionar outra linha permitindo a entrada da segunda data.  
  
 **Valor**  
 Digite o valor para comparar à propriedade. Para datas, clique na seta para baixo para mostrar um calendário para selecionar a data.  
  
 **Limpar Filtro**  
 Remove todas as configurações de filtro atuais.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar SQL Server Management Studio](../sql-server-management-studio-ssms.md)   
 [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
