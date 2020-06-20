---
title: Caixa de diálogo Adicionar tabela (designers de consulta e exibição) (ferramentas de banco de dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8d7bf30cbdd37927735c36f184208a1ded957763
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058227"
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>Caixa de diálogo Adicionar Tabela (Designers de Consulta e Exibição) (Visual Database Tools)
  Essa caixa de diálogo permite que você adicione tabelas, exibições, funções definidas pelo usuário ou sinônimos a uma consulta ou exibição.  
  
> [!NOTE]  
>  Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
 **Tabelas**  
 Lista as tabelas que você pode adicionar ao painel **Diagrama** . Para adicionar uma tabela, selecione-a e clique em **Adicionar**. Para adicionar várias tabelas de uma vez, selecione-as e clique em **Adicionar**.  
  
 **Exibições**  
 Lista os modos de exibição que você pode adicionar ao painel **Diagrama** . Para adicionar um modo de exibição, selecione-o e clique em **Adicionar**. Para adicionar vários modos de exibição de uma vez, selecione-os e clique em **Adicionar**.  
  
 **Funções**  
 Lista as funções definidas pelo usuário que você pode adicionar ao painel **Diagrama** . Para adicionar uma função, selecione-a e clique em **Adicionar**. Para adicionar várias funções de uma vez, selecione-as em clique em **Adicionar**.  
  
 **Sinônimos**  
 Lista os sinônimos que você pode adicionar ao painel **Diagrama** . Para adicionar um sinônimo, selecione-o e clique em **Adicionar**. Para adicionar vários sinônimos de uma vez, selecione-os em clique em **Adicionar**.  
  
 **Atualizar**  
 Atualiza a lista para incluir qualquer alteração feita ao banco de dados desde que a lista foi recuperada pela última vez.  
  
 **Adicionar**  
 Adiciona o item ou itens selecionados.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
