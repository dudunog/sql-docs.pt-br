---
title: Inserir snippets Transact-SQL com Surround
description: Saiba como inserir um snippet Surround With para funcionar como ponto de partida para a colocação de instruções em blocos de código.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- snippets [Transact-SQL], surround with
- IntelliSense [SQL Server], surround with snippets
- Transact-SQL snippets, surround with
ms.assetid: 5b5a8c6c-968e-4361-a7f5-9e2ac186d927
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a97616d707849e94de995e29bda6b7853f6631d7
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901932"
---
# <a name="insert-surround-with-transact-sql-snippets"></a>Inserir snippets Transact-SQL com Surround
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Um snippet com surround é um modelo que você pode usar como ponto de partida ao colocar um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um bloco BEGIN, IF ou WHILE.  
  
## <a name="inserting-surround-with-snippets"></a>Inserindo snippets com surround  
 Snippets com surround podem ser iniciados por uma das três maneiras: por meio de um atalho de teclado, menu **Editar** e menu de contexto.  
  
 Após a inserção do snippet, você deve alterar o texto de substituição para formar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida. Para obter mais informações, veja [Concluir snippets Transact-SQL](../../relational-databases/scripting/complete-transact-sql-snippets.md).  
  
#### <a name="to-insert-a-surround-with-snippet"></a>Para inserir um snippet com surround  
  
1.  Na janela Editor de Consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , selecione o conjunto de instruções a serem incluídas no bloco.  
  
2.  Use um destes três métodos para exibir a lista de snippets com surround:  
  
    -   Digite CTRL+K, CTRL+S.  
  
    -   No menu **Editar** , aponte para **IntelliSense**e selecione o comando **Surround With** .  
  
    -   Clique com o botão direito do mouse no texto selecionado e selecione o comando **Surround With** no menu de contexto.  
  
3.  Selecione o nome do snippet (BEGIN, IF ou WHILE) na lista usando o mouse ou digitando-o e pressionando TAB ou ENTER.  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir snippets Transact-SQL](../../relational-databases/scripting/insert-transact-sql-snippets.md)  
  
  
