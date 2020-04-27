---
title: Gráfico de precisão (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- mining models, validating
- mining models, charting
- lift chart
- mining models, testing
- lift [data mining]
ms.assetid: 303973b4-71c0-4cfc-b7bc-92218b52509d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebe159aed7b27bf00ef47a110de1c7ec5ee70adb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062985"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>Gráfico de Precisão (Suplementos de Mineração de Dados do SQL Server)
  ![Botão Gráfico de Precisão na faixa de opções Mineração de Dados](media/dmc-accchart.gif "Botão Gráfico de Precisão na faixa de opções Mineração de Dados")  
  
 Um gráfico de precisão lhe permite aplicar um modelo a um novo conjunto de dados e avaliar a execução desse modelo. O gráfico de exatidão criado por esse assistente é um *gráfico*de comparação de precisão, que é um tipo de gráfico que é frequentemente usado para medir a precisão de um modelo de data mining. Esse tipo de gráfico de precisão exibe uma representação gráfica da melhoria obtida com o uso do modelo de mineração de dados especificado, em comparação com previsões aleatórias e com o caso ideal em que 100% das previsões são precisas. Você pode comparar vários modelos em um único gráfico.  
  
## <a name="example"></a>Exemplo  
 Considere o caso em que o Departamento de marketing da Adventure Works Cycles deseja criar uma campanha de correspondência direcionada. Das campanhas anteriores eles sabem que é típica uma taxa de resposta de 10 por cento. Eles têm uma lista de 10.000 clientes potenciais armazenada em uma tabela do banco de dados. Considerando a taxa de resposta típica, eles podem esperar que 1.000 clientes respondam.  
  
 No entanto, como não pode custear o envio de propaganda pelo correio para apenas 5.000 clientes, o departamento de Marketing usa um modelo de mineração para se dirigir aos 5.000 clientes com maior probabilidade de responder.  
  
 Se a empresa selecionar aleatoriamente 5.000 clientes, pode esperar receber apenas 500 respostas positivas, porque somente 10% do público responderá geralmente. Este cenário é representado pela linha aleatório no gráfico de comparação de precisão.  
  
 No entanto, se o Departamento de marketing usar um modelo de mineração para direcionar a correspondência e se esse modelo estava perfeito, a empresa poderá esperar receber 1.000 respostas ao enviar um anúncio aos 1.000 clientes potenciais recomendados pelo modelo. Este cenário é representado pela linha ideal no gráfico de comparação de precisão.  
  
## <a name="using-the-accuracy-chart-wizard"></a>Usando o Assistente de Gráfico de Precisão  
 Para criar um gráfico de precisão, você deve referenciar uma estrutura de mineração de dados existente. Você pode medir a precisão de vários modelos com base nessa estrutura, desde que eles prevejam a mesma coisa.  
  
 Se você não tiver certeza sobre quais estruturas estão disponíveis, procure no servidor. Para obter mais informações, consulte [procurando modelos no Excel &#40;SQL Server suplementos de mineração de dados&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-an-accuracy-chart"></a>Para criar um gráfico de precisão  
  
1.  Clique na faixa de faixas **cliente de mineração de dados** .  
  
2.  No grupo de **precisão e validação** , clique em **gráfico de precisão**.  
  
3.  Na caixa de diálogo **selecionar estrutura ou modelo** , escolha o modelo que você deseja avaliar. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Escolha um modelo bem parecido com os dados que você pretende testar.  
  
4.  Na caixa de diálogo **especificar coluna para prever e valor a prever** , escolha a coluna que você deseja prever e um valor de destino, se apropriado. Clique em **Avançar**.  
  
     No exemplo acima, você pode escolher a coluna que modela a resposta do cliente e especificar o valor de destino como "Probabilidade de compra".  
  
    > [!NOTE]  
    >  Não é possível prever um valor contínuo. No entanto, você pode discretizar a coluna separando os valores em intervalos discretos. Faça isso antes de criar o modelo de mineração de dados.  
  
5.  Na caixa de diálogo **selecionar dados de origem** , especifique a origem dos dados que você passará pelo modelo para criar uma previsão.  
  
6.  Se você estiver usando uma fonte de dados externa, e não os dados de teste que são armazenados com o modelo, na caixa de diálogo **especificar relações** , mapeie as colunas nos novos dados de origem para as colunas usadas no modelo de data mining.  
  
     Se os nomes das colunas forem semelhantes, eles serão mapeados automaticamente pelo assistente. Embora algumas colunas nos dados de entrada talvez sejam irrelevantes para análise e possam ser ignoradas, algumas colunas são necessárias para que o modelo de mineração de dados processe a entrada. Essas colunas podem incluir uma ID de transação, o valor de destino ou colunas usadas para previsão. Se você não conseguir mapear uma coluna necessária, o assistente fornecerá uma mensagem de aviso.  
  
7.  Clique em **Concluir**.  
  
     O assistente cria um relatório que contém o gráfico de comparação de precisão e os dados subjacentes.  
  
### <a name="requirements"></a>Requisitos  
 Se você estiver prevendo um valor discreto, selecione o valor de destino que deseja prever. Por exemplo, se os dados estiverem categorizados com uma resposta "Sim: Comprar" como 1 e a resposta "Não: Não Comprar" como 2, você deve especificar 1 ou 2 como valores de previsão. No entanto, se você quiser prever um intervalo de valores, compare apenas dois valores de cada vez. Por exemplo, para prever uma pontuação acima de 5, talvez seja necessário rotular novamente os dados de origem e criar um novo modelo que separa os resultados em dois conjuntos: aqueles maiores do que 5 e os menores do que 5. Você pode comparar a precisão desses dois grupos.  
  
## <a name="understanding-accuracy"></a>Entendendo a precisão  
 É possível criar dois tipos de gráficos: um no qual você especifica um estado da coluna previsível e outro no qual não especifica o estado.  
  
 Se você especificar o estado da coluna previsível, o eixo x do gráfico representará a porcentagem do conjunto de dados de teste usado para comparar as previsões. O eixo y do gráfico representa a porcentagem de valores previstos para ser o estado especificado.  
  
 Se você não especificar o estado da coluna previsível, o gráfico mostrará a precisão do modelo para todas as previsões possíveis.  
  
 Para obter mais informações sobre como um gráfico de comparação de precisão funciona e como a precisão é calculada com base nas linhas de previsão aleatória e ideal, consulte o tópico "Gráfico de comparação de precisão" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Validando modelos e usando modelos para previsão &#40;suplementos de mineração de dados para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
