---
title: Adicionar medidores a relatórios móveis | Reporting Services | Microsoft Docs
description: Você pode adicionar medidores a um relatório móvel do Reporting Services. Os medidores exibem um valor em um conjunto de dados em si só ou em comparação a uma meta.
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 456c50650afc01fc18465b0d96f3cfeb715ddecb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448285"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>Adicionar medidores a relatórios móveis | Reporting Services
Medidores são os visuais mais básicos e amplamente usados em relatórios móveis. Eles exibem um único valor em um conjunto de dados – apenas o valor ou o valor comparado a uma meta.

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*Visualizações de medidor na guia Layout*  
  
No Publicador de Relatórios Móveis do Microsoft SQL Server, todos os medidores têm pelo menos uma propriedade em comum: um valor principal, definido como um campo numérico em uma das tabelas de dados no relatório móvel.  

Todos os medidores, exceto pelo medidor de Número, também podem exibir um valor de comparação, ou *delta*, – a relação entre o valor principal e um valor de comparação. O valor de comparação é, muitas vezes, o objetivo e o medidor é um indicador visual do progresso para esse objetivo, ou o delta entre o valor real e o objetivo.

Os medidores só podem representar um valor agregado para o valor principal e um valor agregado para o valor de comparação. As agregações de medidor são padrão – soma, média, mínimo, máximo e assim por diante. Por padrão, o valor do medidor é uma soma, que exibe o total de todos os valores contidos nos dados filtrados atuais disponíveis no controle do medidor. 

Você pode filtrar os valores de medidor conectando-os a navegadores no relatório móvel. 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>Definir os valores de comparação e principal para um medidor

1. Arraste um medidor da guia **Layout** para a grade de design e deixe-a do tamanho desejado.

2. Obter [dados do Excel ou de um conjunto de dados compartilhado](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. Selecione a guia **Dados** e, no painel **Propriedades de dados** , em **Valor Principal** , selecione uma tabela de dados e um campo numérico.

3. Em qualquer medidor, exceto pelo medidor de Número, no painel **Propriedades de dados** , em **Valor de Comparação** , selecione uma tabela de dados e um campo numérico.

4. [opcional] Para alterar a agregação, selecione **Opções** e selecione uma agregação diferente.
   
   >**Observação**: quando alterar a agregação para o valor principal, provavelmente você também precisará alterar a agregação para o valor de comparação, embora em alguns casos você possa querer combinar os métodos de agregação.  

## <a name="filter-a-gauge"></a>Filtrar um medidor
  
Se o relatório móvel tiver navegadores, você poderá associar um medidor a um ou mais deles para filtrá-los. Você pode associar o valor e o valor de comparação de um medidor a um ou mais navegadores diferentes, o que leva a opções quase intermináveis de medidores.  

1. Selecione um medidor e, na guia **Dados** do painel **Propriedades de dados** , selecione **Opções** ao lado de **Valor Principal** ou **Valor de Comparação**.

2. Em Filtrado por, selecione o navegador que você deseja filtrar o medidor.

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>Definir propriedades visuais para um medidor
  
Juntamente com as propriedades de dados que se conectam a elementos de medidor para campos de dados, você também pode personalizar algumas propriedades funcionais e visuais. 

### <a name="set-value-direction-high-or-low-is-better"></a>Definir a direção de valor: alto ou baixo é melhor
* Selecione um medidor e, na guia **Layout** no painel **Propriedades Visuais** , defina **Direção do valor** como **Valores mais altos são melhores** ou **Valores mais baixos são melhores**. 

**Valores mais altos são melhores** colore os valores positivos em verde, indicando uma alteração desejável para melhor, ou em vermelho, indicando uma alteração indesejável para pior. 

As cores para **Valores mais baixos são melhores** são o oposto.

A propriedade de direção de valor tem relação apenas com elementos de Medidor que dão suporte a um valor de comparação. A cor do medidor é determinada pelo sinal do inteiro do delta e pela configuração de propriedade de direção do valor.  
  
### <a name="set-range-stops-for-a-gauge"></a>Definir interrupções de intervalo para um medidor
A segunda propriedade sem dados específica de medidor é de paradas de intervalo. 

* Selecione um medidor e, na guia **Layout** no painel **Propriedades visuais** , selecione **Interrupções de intervalo**.

Com interrupções de intervalo, você determina em qual percentual de seu valor de comparação a visualização deve ser apresentada como no destino (verde), neutra (âmbar) ou fora do destino (vermelho); sendo o destino um valor de comparação do indicador. Mais uma vez, apenas medidores com valores de comparação dão suporte a interrupções de intervalo.  

### <a name="format-the-numbers-in-the-gauge"></a>Formatar os números no medidor  
Outra propriedade sem dados do elemento de medidor que é compartilhada por muitos outros elementos é o formato de número. 

* Selecione um medidor e, na guia **Layout** no painel **Propriedades visuais** , selecione **Interrupções de intervalo**.

Ela determina como os números exibidos no medidor são formatados – por exemplo, moeda, percentual, hora ou geral. Você define a formatação dos números em cada elemento do relatório móvel.
  
### <a name="see-also"></a>Confira também 

* [Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navegadores nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualizações nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Grades de dados nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
