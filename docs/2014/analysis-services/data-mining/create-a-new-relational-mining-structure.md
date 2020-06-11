---
title: Criar uma nova estrutura de mineração relacional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], relational
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
ms.assetid: 55bac3bd-700e-4f91-bcc6-f3cd8c026da1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 534b27d024feb521be133329c7fe0aef06d9814a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523872"
---
# <a name="create-a-new-relational-mining-structure"></a>Criar uma nova estrutura de mineração relacional
  Use o assistente de mineração de dados para criar uma nova estrutura de mineração, usando dados de um banco de dado relacional ou outra fonte e, em seguida, salve a estrutura e todos os modelos relacionados em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados.  
  
### <a name="to-create-a-relational-mining-structure"></a>Para criar uma estrutura de mineração relacional  
  
1.  No gerenciador de soluções, clique com o botão direito do mouse na pasta **Estruturas de Mineração** no projeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e depois clique em **Nova Estrutura de Mineração**.  
  
     O Assistente de Mineração de Dados é exibido.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Definição** , selecione **De banco de dados relacional ou data warehouse existente**e clique em **Avançar**.  
  
4.  Na página **Selecionar Técnica de Mineração de Dados** , selecione o algoritmo de mineração de dados que deseja usar e clique em **Avançar**.  
  
     Para obter mais informações sobre os algoritmos de mineração de dados, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Na página **Selecionar a Exibição da Fonte de Dados** , em **Exibições de fonte de dados disponíveis**, clique na exibição da fonte de dados que deseja usar e, em seguida, clique em **Avançar**.  
  
     Para obter mais informações sobre exibições de fonte de dados, consulte [Exibições de Fonte de Dados em Modelos Multidimensionais](../multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
6.  Na página **Especificar Tipos de Tabelas** , em **Tabelas de entrada**, selecione uma tabela de casos e uma tabela aninhada.  
  
7.  Na página **Especificar os Dados de Treinamento** , em **Estrutura de modelo de mineração**, selecione as colunas de chave, de entrada e as colunas previsíveis.  
  
     Depois de selecionar a coluna previsível, você pode clicar no botão **Sugerir** para abrir a caixa de diálogo **Sugerir Colunas Relacionadas** . Você pode aceitar as colunas sugeridas clicando em **OK** nessa caixa de diálogo, para incluir as colunas selecionadas na estrutura de mineração ou pode alterar as seleções na coluna **Entrada** primeiro e, em seguida, clicar em **OK**. Para ignorar as sugestões, clique em **Cancelar**.  
  
8.  Clique em **Próximo**.  
  
9. Na página **Especificar Conteúdo e Tipos de Dados das Colunas** , em **Estrutura de modelo de mineração**, você pode ajustar o tipo de conteúdo e o tipo de dados para cada coluna.  
  
    > [!NOTE]  
    >  Você pode clicar em **Detectar** para detectar automaticamente se uma coluna contém dados contínuos ou distintos. Depois de clicar nesse botão, o conteúdo e os tipos de dados da coluna serão atualizado nas colunas **Tipo de Conteúdo** e **Tipo de Dados** . Para obter mais informações sobre tipos de conteúdo e de dados, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](content-types-data-mining.md) e [Tipos de dados &#40;Mineração de dados&#41;](data-types-data-mining.md).  
  
10. Clique em **Próximo**.  
  
11. Na página **Concluindo o Assistente** , forneça um nome para a estrutura de mineração e o modelo de mineração inicial correspondente a ser criado e, em seguida, clique em **Concluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
