---
title: Cenário de busca de meta (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d547c52bc5d4cb02870fc647469b5f63af9ab7cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080735"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>Cenário de Metas a Atingir (Ferramentas de Análise de Tabela para Excel)
  ![Botão Meta a Atingir em Ferramentas de Análise de Tabela](media/tat-goalseek.gif "Botão Meta a Atingir em Ferramentas de Análise de Tabela")  
  
 A ferramenta de cenário de **busca de meta** é complementar à ferramenta de cenário de [What If](what-if-scenario-table-analysis-tools-for-excel.md) . A ferramenta **What-If** indica o impacto de fazer uma alteração, enquanto a ferramenta **meta Seek** informa os fatores subjacentes que devem ser alterados para obter um resultado desejado.  
  
 Por exemplo, digamos que seu objetivo seja aumentar a satisfação do cliente. Você pode usar a análise de **meta Seek** para determinar quais fatores são mais prováveis de aumentar a satisfação do cliente e decidir se essas alterações são econômicas.  
  
 Quando a ferramenta conclui sua análise, ela cria duas colunas novas na tabela de dados de origem. Essas colunas mostram a *probabilidade* de que o resultado de destino possa ser obtido e a alteração recomendada, se houver.  
  
 A ferramenta pode analisar um conjunto de dados e fazer previsões para todo o conjunto ou você pode criar a análise e testar os cenários um de cada vez.  
  
## <a name="using-the-goal-seek-scenario-tool"></a>Usando a ferramenta de cenário Meta a Atingir  
  
1.  Abra uma tabela do Excel.  
  
2.  Clique em **cenários**e selecione **meta buscar**.  
  
3.  Na caixa de diálogo **análise de cenário: meta de busca** , selecione a coluna que contém o valor de destino da lista.  
  
4.  Especifique o valor que você deseja atingir.  
  
     Se a meta da coluna contiver valores numéricos contínuos, também será possível especificar uma diminuição ou um aumento desejado no valor. Por exemplo, você pode escolher **vendas** como a coluna e especificar que o destino é um aumento de 120%.  
  
     Ou, você pode especificar a meta como um intervalo de valores, digitando um limite inferior e um limite superior.  
  
5.  Especifique a coluna que contém os valores que serão alterados. Em outras palavras, escolha a coluna que será manipulada para produzir o resultado desejado.  
  
6.  Opcionalmente, clique em **escolher colunas a serem usadas para análise**e selecione as colunas que contêm informações úteis. Desmarque as colunas que não colaborarão para a análise.  
  
    > [!NOTE]  
    >  Não desmarque colunas que você usará para a meta ou a alteração. Essas colunas são necessárias.  
  
7.  Especifique se você deseja fazer previsões para toda a tabela ou apenas para a linha selecionada.  
  
8.  Se você selecionou a opção de **tabela inteira** , a ferramenta adicionará as previsões à tabela de origem em duas novas colunas.  
  
9. Se você selecionou a opção **nessa linha**, os resultados da análise serão gerados para a caixa de diálogo para revisão. A caixa de diálogo permanece aberta para que você possa continuar experimentando valores e metas diferentes.  
  
### <a name="requirements"></a>Requisitos  
 Essa ferramenta usa o algoritmo Regressão Logística da Microsoft, que pode processar valores numéricos ou discretos.  
  
 Você pode executar a previsão várias vezes e selecionar colunas diferentes depois, mas cada combinação de meta e alteração deve ser calculada separadamente.  
  
 Você poderá obter resultados melhores se selecionar colunas para análise que contenham informações úteis. No entanto, se você incluir poucas colunas, talvez seja difícil obter um resultado.  
  
 Quando você criar uma previsão de cada vez, não se esqueça de selecionar uma linha que ainda não contenha o resultado desejado ou talvez receba um erro. Em outras palavras, se a finalidade da meta a atingir for determinar fatores que incentivem compras de bicicletas, inclua apenas clientes que não compraram uma bicicleta.  
  
## <a name="understanding-the-results-of-goal-seek-analysis"></a>Compreendendo os resultados da análise Meta a Atingir  
 Quando você cria um cenário Meta a Atingir, a ferramenta executa três ações:  
  
-   Cria uma estrutura de mineração de dados que armazena os fatos principais sobre os dados na tabela.  
  
-   Cria um modelo de mineração de regressão logística com base nos dados.  
  
-   Cria uma previsão para cada valor especificado.  
  
 Se você testar os cenários de meta a atingir um de cada vez, poderá exibir os resultados interativamente. Isso é o mesmo que criar uma *consulta de Previsão Singleton*.  
  
 A ferramenta relata no painel de **resultados** da caixa de diálogo se foi bem-sucedida ao encontrar um cenário que atinja a meta desejada. Caso uma solução bem-sucedida tenha sido encontrada, a ferramenta também gerará uma recomendação informando sobre a alteração necessária. Por exemplo, a ferramenta de **busca de meta** pode informar que a distância de comutação deve ser inferior a 5 milhas.  
  
 Resultados do exemplo:  
  
 **A opção Meta a Atingir de Interesse na Compra encontrou uma solução.**  
  
 **A correspondência mais próxima obtida com a alteração de 'Commute distance' para '2-5 miles'.**  
  
 Como esse resultado se baseia em uma linha existente na tabela de dados, isso significa que, para um determinado cliente, se todos os dados referentes ao cliente permanecerem iguais, mas a distância do trabalho do cliente for reduzida para 2-5 miles, ele provavelmente ficará um pouco mais inclinado a comprar uma bicicleta.  
  
 Se você criar previsões de meta-busca para todas as linhas na tabela do Excel especificando a **tabela inteira**, a ferramenta criará duas novas colunas na tabela de dados original. A primeira coluna adicionada à tabela contém uma marca de seleção em um círculo verde, para indicar que a meta pode ser alcançada, ou um X em um círculo vermelho, para indicar que não é possível fazer nenhuma alteração para permitir a meta.  
  
 A segunda coluna contém a alteração recomendada.  
  
> [!NOTE]  
>  O nível de confiança da recomendação e seu êxito são predeterminados pelo algoritmo e não podem ser alterados.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece mais funções avançadas de mineração de dados, contém assistentes para criação de modelos de mineração de dados que preveem comportamento. Para obter mais informações, consulte [criando um modelo de mineração de dados](creating-a-data-mining-model.md).  
  
 Para obter mais informações sobre o algoritmo usado pela ferramenta de cenário de **busca de meta** , consulte o tópico "algoritmo de regressão [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] logística da Microsoft" nos manuais online do.  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
