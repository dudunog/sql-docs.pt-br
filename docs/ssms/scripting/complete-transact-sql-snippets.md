---
title: Concluir snippets Transact-SQL
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2109b236bc13e8335e619ed90b8ee9a33ca08844
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253998"
---
# <a name="complete-transact-sql-snippets"></a>Concluir snippets Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Quando um snippet de código [!INCLUDE[tsql](../../includes/tsql-md.md)] foi inserido em um script, você edita o conteúdo do snippet para compilar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa.  
  
## <a name="completing-snippets"></a>Concluindo snippets  
 Quando você acrescentar um snippet [!INCLUDE[tsql](../../includes/tsql-md.md)] ao seu script, a instrução de snippet inserida terá um ou mais pontos de substituição, que serão destacados. Se você posicionar o seu ponteiro do mouse em um ponto de substituição, uma dica de ferramenta aparecerá com uma descrição do elemento de sintaxe que você pode especificar. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] Editor de Consulta reconhece o snippet como separado do script ao redor até que você feche o arquivo de origem. Os pontos de substituição permanecem ativos até que você feche o arquivo de origem.  
  
 Você também pode acrescentar elementos de sintaxe adicionais ao código de modelo inserido por um snippet. Por exemplo, o modelo Criar Snippet de Tabela gera duas definições de coluna; você deve adicionar outras definições de coluna para criar uma tabela com mais de duas colunas.  
  
#### <a name="completing-the-snippet-statement"></a>Concluindo a instrução de snippet  
  
1.  Use a tecla TAB para se mover de um ponto de substituição ao próximo. Use SHIFT+TAB para se mover para o ponto de substituição anterior.  
  
2.  Clique em CTRL+SPACE para invocar IntelliSense.  
  
3.  Selecione um item da lista ou digite uma substituição de sua escolha.  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir snippets Transact-SQL](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [Inserir snippets Transact-SQL com Surround](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
