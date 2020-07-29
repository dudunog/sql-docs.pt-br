---
title: Criar consultas de atualização
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 85dbdecd8b20ff27eb74c4078fca81dcbc39d53e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999972"
---
# <a name="create-update-queries-visual-database-tools"></a>Criar consultas de atualização (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode alterar o conteúdo de várias linhas em uma operação usando uma consulta Update. Por exemplo, em uma tabela `titles` , você pode usar uma consulta Update para adicionar 10% ao preço de todos os livros de um publicador específico.  
  
Ao criar uma consulta Update, você especifica:  
  
-   A tabela a ser atualizada.  
  
-   As colunas cujo conteúdo você deseja atualizar.  
  
-   O valor ou a expressão a ser atualizada nas colunas individuais.  
  
-   Os critérios de pesquisa para definir as linhas que você deseja atualizar.  
  
Por exemplo, a consulta seguinte atualiza a tabela `titles` adicionando 10% ao preço de todos os títulos de um publicador:  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
> Você não pode desfazer a ação de execução da consulta Update. Como precaução, faça backup de seus dados antes de executar a consulta.  
  
### <a name="to-create-an-update-query"></a>Para criar uma consulta Update  
  
1.  Adicione a tabela que deseja atualizar ao painel Diagrama.  
  
2.  No menu **Designer de Consultas** , aponte para **Alterar Tipo**e clique em **Atualizar**.  
  
    > [!NOTE]  
    > Se mais de uma tabela for exibida no painel Diagrama quando você iniciar a consulta de Atualização, o Designer de Consulta e Exibição exibirá [Escolher Tabela de Destino da Caixa de Diálogo Inserir Valores](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) , que solicitará o nome da tabela a ser atualizada.  
  
3.  No painel Diagrama, clique na caixa de seleção de cada coluna para a qual você deseja fornecer novos valores. Essas colunas serão exibidas no painel Critérios. As colunas só serão atualizadas se você as adicionar à consulta.  
  
4.  Na coluna **Novo Valor** do painel Critérios, insira o valor de atualização para a coluna. Você pode inserir valores literais, nomes de coluna ou expressões. O valor deve corresponder (ou ser compatível com) ao tipo de dados da coluna que você está atualizando.  
  
    > [!CAUTION]  
    > O Designer de Consulta e Exibição não pode verificar se um valor é adequado ao comprimento da coluna que você está atualizando. Se você fornecer um valor muito longo, ele poderá ser truncado sem aviso. Por exemplo, se uma coluna `name` tiver 20 caracteres, mas você especificar um valor de atualização de 25 caracteres, os últimos 5 caracteres poderão ser truncados.  
  
5.  Defina as linhas a serem atualizadas inserindo critérios de pesquisa na coluna **Filtro**. Para obter detalhes, consulte [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Se você não especificar um critério de pesquisa, todas as linhas na tabela especificada serão atualizadas.  
  
    > [!NOTE]  
    > Quando você adiciona uma coluna ao painel Critérios para uso em um critério de pesquisa, o Designer de Consulta e Exibição também a adiciona à lista de colunas a serem atualizadas. Se você quiser utilizar uma coluna para um critério de pesquisa, mas não quiser atualizá-la, desmarque a caixa de seleção próxima ao nome da coluna no retângulo que representa a tabela ou o objeto com valor de tabela.  
  
Quando você executa uma consulta de Atualização, nenhum resultado será relatado no painel de [Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando quantas linhas foram alteradas.  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
