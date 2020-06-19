---
title: Selecionar as tabelas Oracle para capturar alterações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 42bc0e1533e53b6a8f52b6ba71f0a128575e7448
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84922457"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>Selecionar as tabelas Oracle para capturar alterações
  Use esta caixa de diálogo para selecionar as tabelas incluídas na instância CDC. As tabelas selecionadas são adicionadas à lista na página **Selecionar Tabelas e Colunas** do Assistente de Nova Instância. É possível fazer o seguinte nesta caixa de diálogo.  
  
 Por padrão, nenhuma tabela está incluída na lista de tabelas nesta caixa de diálogo. Você pode marcar a caixa de seleção na parte superior da coluna de caixa de seleção para selecionar todas as tabelas ou procurar tabelas específicas.  
  
 **Para pesquisar tabelas específicas**  
 Insira os critérios de pesquisa da seguinte maneira e clique em **Pesquisar**:  
  
-   **Esquema**: selecione um esquema de banco de dados da lista. Somente tabelas que têm esquema serão incluídas na lista.  
  
-   **Padrão de Nome de Tabela**: insira qualquer cadeia de caracteres. Somente tabelas que incluem a cadeia de caracteres inserida serão exibidas.  
  
> [!NOTE]  
>  Você pode inserir critérios em um ou ambos os campos.  
  
-   **Exibir as 1000 primeiras tabelas correspondentes**: por padrão, esta caixa de seleção está marcada. Limita o vídeo às primeiras 1000 tabelas compatíveis. Se você desmarcar a caixa de seleção, todas as tabelas que correspondem aos critérios serão exibidas. Se houver um número grande de tabelas, poderá levar muito tempo para exibir a lista.  
  
 **Para selecionar tabelas a serem incluídas na instância CDC**  
 Clique na caixa de seleção ao lado de qualquer uma das tabelas que você quer incluir e clique em **Adicionar**. As tabelas são adicionadas à lista na página **Selecionar Tabelas e Colunas** do Assistente de Nova Instância.  
  
 Clique em **Fechar** para fechar a caixa de diálogo sem adicionar tabelas.  
  
> [!NOTE]  
>  Se você selecionar uma tabela que inclui um tipo de dados sem suporte, verá uma mensagem de erro e a tabela não será incluída.  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Selecionar tabelas e colunas Oracle](select-oracle-tables-and-columns.md)  
  
  
