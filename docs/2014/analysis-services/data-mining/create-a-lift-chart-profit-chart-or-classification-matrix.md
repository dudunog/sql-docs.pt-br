---
title: Criar um gráfico de comparação de precisão, gráfico de ganho ou matriz de classificação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
author: minewiskan
ms.author: owend
ms.openlocfilehash: 82514e49b8e991c45bab4d1c32365765cefeeb65
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523882"
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>Criar um gráfico de comparação de precisão, gráfico de lucro ou matriz de classificação
  Você pode criar um gráfico de precisão de um modelo de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em cinco etapas básica:  
  
-   Selecione a estrutura de mineração que contém os modelos de mineração que deseja comparar.  
  
-   Selecione os modelos de mineração a serem adicionados ao gráfico.  
  
-   Especifique uma fonte de dados de teste para usar na geração do gráfico.  
  
-   Escolha o tipo de gráfico.  
  
-   Configure as opções de gráfico.  
  
 Estas etapas básicas são iguais para o gráfico de comparação de precisão, o gráfico de ganho e a matriz de classificação. Os procedimentos a seguir descrevem as etapas para configurar as opções básicas para estes tipos de gráfico. Para obter informações sobre como criar um relatório de validação cruzada, consulte [Medidas no relatório de validação cruzada](measures-in-the-cross-validation-report.md).  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>Abra a estrutura de mineração no Designer de Gráficos de Precisão  
  
1.  Abra o Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  No Gerenciador de Soluções, clique duas vezes na estrutura que contém os modelos de mineração.  
  
3.  Clique na guia **Gráfico de Precisão de Mineração** .  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>Selecione modelos de mineração para inclusão no gráfico  
  
1.  Na guia **Gráfico de Precisão de Mineração** do Designer de Data Mining no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na guia **Seleção de Entrada** .  
  
     A lista exibe todos os modelos da estrutura atual que têm o mesmo atributo previsível.  
  
2.  Selecione a caixa **Mostrar** de cada modelo que deseja incluir no gráfico.  
  
3.  Clique na caixa de texto **Nome da Coluna Previsível** e selecione o nome de uma coluna previsível da lista. Todos os modelos incluídos no gráfico devem usar a mesma coluna previsível.  
  
4.  Se você comparar dois modelos e as colunas previsíveis tiverem valores diferentes ou tipos de dados diferentes, desmarque a caixa **Sincronizar colunas de valores de previsão** para forçar uma comparação.  
  
    > [!NOTE]  
    >  Se a caixa **Sincronizar colunas de valores de previsão** estiver selecionada, o Analysis Services analisará os dados na coluna previsível do modelo e os dados de teste, e tentará encontrar a melhor correspondência. Portanto, não desmarque a caixa a menos que seja absolutamente necessário forçar uma comparação das colunas.  
  
5.  Clique na caixa de texto **Valor de Previsão** e selecione um valor da lista. Se a coluna previsível for um tipo de dados contínuo, você deve digitar um valor na caixa de texto.  
  
     Para obter informações, consulte [Escolher a coluna a ser usada em um teste de modelo de mineração](choose-the-column-to-use-for-testing-a-mining-model.md).  
  
### <a name="select-testing-data"></a>Selecionar dados de teste  
  
1.  Na guia **Seleção de Entrada** da guia **Gráfico de Precisão de Mineração** , especifique a fonte de dados que será usada para gerar o gráfico selecionando uma das opções do grupo, **Selecionar conjunto de dados a ser usado para o gráfico de precisão**.  
  
    -   Selecione a opção, **Usar casos de teste do modelo de mineração**, se desejar usar o subconjunto de casos definido pela interseção de casos de teste da estrutura de mineração e quaisquer filtros que tenham sido aplicados durante a criação do modelo.  
  
    -   Selecione a opção, **Usar casos de teste da estrutura de mineração**, para usar o conjunto completo de casos de teste definido como parte do conjunto de dados de controle de estruturas de mineração.  
  
    -   Selecione a opção **Especificar um conjunto de dados diferente**se você quiser usar dados externos.  O conjunto de dados deve estar disponível como uma exibição da fonte de dados.   Clique no botão procurar (**...**) para escolher as tabelas de dados a serem usadas para o gráfico de precisão. Para obter mais informações, consulte [Escolher e mapear dados de teste de modelo](choose-and-map-model-testing-data.md).  
  
         Se você estiver usando um conjunto de dados externo, poderá filtrar, se desejar, o conjunto de dados de entrada. Para obter mais informações, consulte [Aplicar filtros aos dados de teste de modelo](apply-filters-to-model-testing-data.md).  
  
> [!NOTE]  
>  Você não pode criar um filtro nos casos de teste do modelo ou nos casos de teste da estrutura de mineração na guia **seleção de entrada** . Para criar um filtro no modelo de mineração, modifique a propriedade Filter do modelo. Para obter mais informações, consulte [Aplicar um filtro a um modelo de mineração](apply-a-filter-to-a-mining-model.md).  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>Definir configurações de gráfico e gerar o gráfico  
  
1.  Na guia **Gráfico de Precisão de Mineração** , clique na guia do gráfico que deseja criar.  
  
2.  Para obter um gráfico de comparação de **precisão**, clique na guia gráfico de comparação de **precisão** . O gráfico é gerado automaticamente com base no modelo, atributos previsíveis e dados de entrada que você acabou de selecionar.  
  
3.  Para uma **matriz de classificação**, clique na guia **matriz de classificação** . Nenhuma configuração adicional é necessária; o gráfico é gerado automaticamente com base nos dados de entrada e no modelo que você selecionou.  
  
4.  Para um **gráfico de ganho**, primeiro clique na guia gráfico de comparação de **precisão** . Em seguida, na lista suspensa **tipo de gráfico** , selecione **gráfico de ganho**.  
  
     Insira as configurações a seguir na caixa de diálogo **Configurações do Gráfico de Ganho** .  
  
     **Média**  
     O número de casos do conjunto de dados que você quer usar ao criar o gráfico de comparação de precisão.  
  
     O modelo sempre escolhe os casos na ordem de probabilidade decrescente, ou seja, se você está avaliando clientes em potencial e escolhe um número que representa somente metade dos registros do seu banco de dados de clientes, o modelo medirá a precisão no subconjunto de casos que melhor se adaptar ao seu modelo.  
  
     Isso acontece porque, ao usar o modelo para gerar uma correspondência ou criar uma campanha, você usa a probabilidade da previsão associada a cada caso para enviar mala direta apenas aos clientes com maior probabilidade de fornecer uma resposta positiva.  
  
     **Custo fixo**  
     O custo fixo associado ao problema empresarial.  
  
     No caso de uma solução de mala direta, o custo fixo poderia representar a taxa de instalação de uma impressora, que é o custo inicial da preparação da mala direta promocional.  
  
     Esse custo se aplica uma vez a toda população alvo.  
  
     **Custo individual**  
     Os custos adicionais ao custo fixo, que podem estar associados a cada contato de cliente. Por exemplo, você poderia inserir o custo da tarifa de correio, no caso de mala direta promocional, ou de ligações telefônicas.  
  
     Esse custo deve ser o mesmo para toda a população alvo. Cada valor é multiplicado pelo número de casos designados.  
  
     **Receita por indivíduo**  
     A receita associada a cada venda bem sucedida.  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;do gráfico de comparação de precisão Analysis Services-Mineração de dados&#41;](lift-chart-analysis-services-data-mining.md)   
 [Matriz de classificação &#40;Analysis Services – Mineração de dados&#41;](classification-matrix-analysis-services-data-mining.md)  
  
  
