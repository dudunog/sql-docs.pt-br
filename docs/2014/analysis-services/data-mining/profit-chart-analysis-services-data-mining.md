---
title: Gráfico de ganho (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy, charting
- revenue, estimating
- benefits, estimating
- charts [Analysis Services]
- profit charts [Analysis Services]
ms.assetid: 760ee051-6fd8-48e3-8d2e-82db3ab45e45
author: minewiskan
ms.author: owend
ms.openlocfilehash: e574aaf4ab748ad61dc47984360e531ca98a3238
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520622"
---
# <a name="profit-chart-analysis-services---data-mining"></a>Gráfico de ganho (Analysis Services - Mineração de dados)
  Um gráfico de ganho exibe a rentabilidade estimada associada ao uso de um modelo de mineração. Por exemplo, vamos supor que seu modelo prevê quais clientes uma empresa deve contatar em um cenário de negócios. Nesse caso, você adicionaria às informações de gráfico de ganho sobre o custo da condução de uma campanha de mala direta. Em seguida, no gráfico completo, você pode consultar o ganho estimado se os clientes são destinados corretamente, em relação a clientes contatados aleatoriamente.  
  
## <a name="build-a-profit-chart"></a>Criar um gráfico de ganho  
 Um gráfico de lucro é semelhante a um gráfico de comparação de precisão. Você inicia criando um gráfico de comparação de precisão e, depois, adiciona as informações de custo e de lucro.  
  
 Para criar um gráfico de ganho, você precisa ter um modelo existente.  
  
 Para este exemplo, usamos o modelo de árvore de decisão Mala Direta. O modelo identifica os clientes que provavelmente comprarão uma bicicleta. Você pode aplicar o **Gráfico de Ganho** para determinar a quantos de seus clientes deve se dirigir para maximizar o ganho.  
  
 Se você não tiver o modelo de exemplo, poderá criá-lo usando o [tutorial de mineração de dados básico](../../tutorials/basic-data-mining-tutorial.md).  
  
1.  Abra o criador de gráfico de precisão de mineração.  
  
    -   No SQL Server Management Studio, clique com o botão direito do mouse no modelo e selecione **Exibir Gráfico de Comparação de Precisão**.  
  
    -   Em SQL Server Data Tools, abra o projeto em que você criou o modelo, e clique na guia **Gráfico de Precisão de Mineração** .  
  
2.  Na guia **Seleção de Entrada** , selecione o modelo e escolha o valor do atributo previsível.  
  
     Para este cenário específico, você está interessado apenas na rentabilidade de prever com precisão um valor: [Bike Buyer] =1.  
  
     No entanto, há outros cenários nos quais você também está interessado em prever valores falsos corretamente. Por exemplo, o custo de um falso positivo em um teste de diagnóstico médico pode ser significativo e precisa ser considerado na rentabilidade da previsão, como ocorre com o custo de falsos negativos. Nesses cenários, você mediria todos os resultados.  
  
3.  Selecione um conjunto de dados para teste. Neste exemplo, selecione o conjunto de dados para teste.  
  
4.  Agora clique na guia **Gráfico de Comparação de Precisão** .  
  
     Um gráfico de comparação de precisão é gerado automaticamente.  
  
5.  Para alterar isso para um gráfico de ganho, selecione **Gráfico de Ganho** na lista **Tipo de gráfico** .  
  
6.  Assim que você escolher o gráfico de ganho como o tipo de gráfico, a caixa de diálogo **Configuração do Gráfico de Ganho** será aberta automaticamente.  
  
     Esta caixa de diálogo ajuda a especificar os custos e os benefícios associados a uma campanha de mala direta. Para o gráfico mostrado nestes exemplos, nós usamos os valores a seguir:  
  
    |Configuração|Valor|Comentários|  
    |-------------|-----------|--------------|  
    |**Média**|20,000|Defina o valor para a população de destino total<br /><br /> Seu banco de dados pode conter muitos clientes, mas, para economizar em despesas de mala direta, você precisa se dirigir apenas aos 20.000 clientes com maior probabilidade de resposta. Você pode obter essa lista executando uma consulta de previsão e classificando pela saída de probabilidade pelo modelo previsível.|  
    |**Custo fixo**|500|Insira o custo único da criação de uma campanha de mala direta para 20.000 pessoas. Isso pode incluir a impressão, ou o custo da criação de uma campanha de email.|  
    |**Custo individual**|3|Insira o custo individual da campanha de mala direta.<br /><br /> Esse valor será multiplicado por um número igual ou inferior a 20.000, dependendo de quantos clientes o modelo prevê como bons clientes potenciais.|  
    |**Receita por indivíduo**|400|Insira um valor que representa a quantidade de lucro ou receita que pode ser esperada de um resultado com êxito. Nesse caso, vamos supor que a correspondência de um catálogo resulta na compra de acessórios ou bicicletas de média de $400.<br /><br /> Essa quantia será usada para projetar o lucro total associado aos casos de alta probabilidade.|  
  
7.  Após definir os parâmetros necessários, clique em **OK**.  
  
8.  O gráfico é atualizado para mostrar a curva de lucro.  
  
## <a name="understanding-the-profit-chart"></a>Entendendo o gráfico de ganho  
 O diagrama a seguir mostra o gráfico que foi baseado nestes parâmetros. O eixo Y do gráfico representa o ganho, enquanto o eixo X representa a porcentagem dos clientes que foram contatados pela campanha de mala direta.  
  
 Como vimos aqui, você pode usar um gráfico de ganho para comparar vários modelos, contanto que todos prevejam o mesmo atributo discreto.  
  
 ![um gráfico de lucros que compara três modelos](../media/dm14-profitchartupdated.gif "um gráfico de lucros que compara três modelos")  
  
 Observe a linha vertical cinza no gráfico. Quando você clicar na linha e arrastá-la, a exibição Dica de Ferramenta exibirá a porcentagem da população de destino que é incluída na curva nesse ponto.  
  
 A **Legenda de Mineração** também é atualizada quando você arrasta a linha, visando refletir o valor percentual, a pontuação de ganho e a probabilidade prevista que associada ao percentual da população na linha vertical cinza.  
  
 Por exemplo, se estiver usando esse modelo para decidir a quem deve enviar o material promocional, você poderá decidir dirigir-se a 25% da população, com base nas probabilidades de previsão. No entanto, a área na curva de lucro do gráfico é maior entre 40% e 70%, indicando que o envio de mala direta a mais pessoas poderá maximizar o retorno, mesmo que uma porcentagem total menor responda.  
  
## <a name="saving-charts"></a>Salvando gráficos  
 Quando você cria um gráfico de precisão ou um gráfico de ganho, nenhum objeto é criado no servidor. Em vez disso, as consultas são executadas em um modelo existente e os resultados são renderizados no visualizador. Se for necessário salvar os resultados, você deverá copiar o gráfico ou os resultados no Excel ou em outro arquivo.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Os tópicos a seguir contêm mais informações sobre como você pode criar e usar gráficos de precisão.  
  
|Tópicos|Links|  
|------------|-----------|  
|Fornece um passo a passo sobre como criar um gráfico de comparação de precisão para o modelo Mala Direta Dirigida.|[Tutorial de mineração de dados básico](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [Testando a precisão com gráficos de comparação de precisão &#40;Tutorial de mineração de dados básica&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|Explica os tipos de gráficos relacionados.|[Gráfico de comparação de precisão &#40;Analysis Services – Mineração de dados&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Matriz de classificação &#40;Analysis Services – Mineração de dados&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [Dispersão &#40;Analysis Services – Mineração de dados&#41;](scatter-plot-analysis-services-data-mining.md)|  
|Descreve validação cruzada para modelos de mineração e estruturas de mineração.|[Validação cruzada &#40;Analysis Services – Data Mining&#41;](cross-validation-analysis-services-data-mining.md)|  
|Descreve as etapas para criar gráficos de comparação de precisão e outros gráficos de exatidão.|[Tarefas de teste e validação e instruções &#40;Mineração de dados&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Teste e validação &#40;mineração de dados&#41;](testing-and-validation-data-mining.md)   
 [Testando a precisão com gráficos de comparação de precisão &#40;Tutorial de mineração de dados básica&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
  
