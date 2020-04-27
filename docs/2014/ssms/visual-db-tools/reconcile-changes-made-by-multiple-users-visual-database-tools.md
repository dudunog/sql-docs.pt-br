---
title: Reconciliar alterações feitas por vários usuários (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f13b7f6a2e34d7819b930d919e9fd773e2c993d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63010679"
---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>Reconciliar alterações feitas por vários usuários (Visual Database Tools)
  Em um ambiente multiusuário, é possível ter vários usuários fazendo alterações no mesmo objeto simultaneamente. Isso pode acontecer quando você estiver trabalhando na estrutura do objeto nos designers de diagrama de banco de dados ou tabela, ou pode ocorrer em valores nos resultados retornados no painel de resultados dos Designers de Consulta e Exibição. Isso pode causar conflitos que devem ser resolvidos.  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>Conflitos nos designers de diagramas de banco de dados ou tabelas  
 Por exemplo, outro usuário pode excluir ou renomear uma tabela enquanto você estiver trabalhando na mesma ou em uma tabela relacionada no Designer de Tabela. Quando você tentar salvar a tabela, a [Caixa de diálogo Alterações no Banco de Dados Detectadas &#40;Visual Database Tools&#41;](visual-database-tools.md) o notifica de que o banco de dados foi atualizado desde que você abriu a tabela.  
  
 Essa caixa de diálogo também exibe uma lista de objetos de banco de dados que serão afetados como resultado de salvar sua tabela. Nesse momento, você pode adotar uma destas ações:  
  
-   Escolha **Sim** para salvar sua tabela e atualizar o banco de dados com todas as alterações na lista.  
  
     Essa ação pode afetar tabelas que compartilham os mesmos objetos de banco de dados. Por exemplo, suponha que você edite a coluna `au`_`id` na tabela `titleauthors` enquanto outro usuário esteja trabalhando na tabela `authors` , que é relacionada à tabela `titleauthors` pela coluna `au`\_`id` . Se você salvar sua tabela, afetará a tabela do outro usuário. De forma semelhante, suponha que outro usuário tenha definido uma restrição de verificação para a coluna `qty` da tabela `sales` . Se você excluir a coluna `qty` e salvar a tabela `sales` , a restrição de verificação do outro usuário será afetada.  
  
-   Selecione **Não** para cancelar a ação.  
  
     Você pode então fechar a tabela sem salvá-la. Quando você reabrir a tabela, ela corresponderá ao que está no banco de dados.  
  
-   Escolha **Salvar Arquivo de Texto** para salvar uma lista das alterações.  
  
     Você pode salvar a lista de alterações do banco de dados mostrada na caixa de diálogo **Alterações no Banco de Dados Detectadas** em um arquivo de texto, de forma que possa investigar a causa das alterações de outros usuários. Por exemplo, se outro usuário tiver editado uma tabela marcada para exclusão, você poderá pesquisar se a tabela deve ser excluída antes de atualizar o banco de dados.  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>Conflitos nos Designers de Consulta e Exibição  
 Se você executar uma consulta ou retornar os resultados de uma exibição, os dados serão mostrados no [Painel de Resultados](results-pane-visual-database-tools.md). Vários usuários podem trabalhar no mesmo conjunto de dados ao mesmo tempo, o que pode causar conflitos.  
  
 Por exemplo, digamos que você e um colega executem uma consulta para mostrar todos os dados da tabela `titleauthors` . Seu colega altera o primeiro nome no primeiro registro retornado de Barb para Bárbara. Nesse momento, o banco de dados tem Bárbara naquele campo, enquanto seu conjunto de resultados ainda mostra Barb. Agora você digita Bárbara e clica fora da linha. Você receberá uma mensagem perguntando como deseja resolver o conflito.  
  
-   Clique em **Sim** para atualizar o banco de dados com suas alterações.  
  
     Isso substituirá as mudanças de seu colega.  
  
-   Clique em **Não** para ter seu conjunto de resultados atualizado ao que está atualmente no banco de dados.  
  
     Isso substituirá suas alterações pelas de seu colega.  
  
-   Clique em **Cancelar** para continuar editando sem resolver o conflito.  
  
     Nesse caso, você não poderá confirmar suas alterações no banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Alterações no Banco de Dados Detectadas &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
