---
title: Explorar dados (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bad2a2e65a65bbafa8218a3e0afbedd4b9f13b6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081315"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>Explorar dados (Suplementos de Mineração de Dados do SQL Server)
  ![Assistente para Explorar Dados](media/dmc-explore.gif "Assistente para Explorar Dados")  
  
 O assistente para **explorar dados** ajuda você a entender o tipo e a quantidade de dados em sua tabela de dados. O assistente representa graficamente a distribuição e os valores das colunas selecionadas, uma coluna por vez. Assim, você pode fazer experiências alterando a maneira como os dados são agrupados ou copiar um gráfico que mostra o conteúdo de uma pasta de trabalho do Excel para análise.  
  
 Se seus dados contiverem dados numéricos contínuos, você poderá ativar /desativar entre essas duas exibições:  
  
-   **Gráfico de linhas.** Esse gráfico de linha coloca os valores de dados no eixo X e o número de casos no eixo Y.  
  
-   **Gráfico de barras.** Esse gráfico agrupa os valores pelo número de casos para cada valor.  
  
 Quando o assistente encontra grupos nos dados, ele usa a distribuição real dos valores de dados. Portanto, o gráfico de barras não mostra marcadores de eixo numérico de número inteiro típicos, como 10 ou 100. Em vez disso, os intervalos mostrados no gráfico de barras podem ser algo como 43521-55603 (para a coluna de renda).  
  
 Se você quiser agrupar os dados em outros intervalos, faça isso no Excel antes de analisar os dados. Ou, você pode rerotular os dados usando o assistente de [rerotulação](relabel-sql-server-data-mining-add-ins.md) .  
  
## <a name="using-the-explore-data-wizard"></a>Usando o Assistente para Explorar Dados  
  
1.  Na faixa de faixas de **mineração de dados** , clique em **explorar dados**.  
  
2.  Na caixa de diálogo **selecionar origem** , selecione a tabela ou o intervalo de células que contém os dados.  
  
3.  Na caixa de diálogo **Selecionar coluna** , escolha a coluna a ser analisada, dos dados de exemplo exibidos no painel.  
  
4.  Na caixa de diálogo **explorar dados** , escolha os tipos de gráfico para exibir a distribuição de dados.  
  
5.  Se desejar, adicione novas colunas aos dados, altere a segmentação dos dados ou copie o gráfico para o Excel.  
  
### <a name="requirements"></a>Requisitos  
 Para usar o assistente para **explorar dados** , seus dados devem estar em uma tabela de dados do Excel.   
  
## <a name="see-also"></a>Consulte Também  
 [Lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md)  
  
  
