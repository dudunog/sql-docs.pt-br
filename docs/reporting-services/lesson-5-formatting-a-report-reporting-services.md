---
title: 'Lição 5: Formatando um relatório (Reporting Services) | Microsoft Docs'
description: Saiba como formatar os campos de data e moeda e os cabeçalhos de coluna depois de adicionar uma região de dados e alguns campos ao relatório de Ordens de Vendas.
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ef2d3fd220aef7a593a2244cf2d7509c5264fcca
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245105"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lição 5: formatar um relatório (Reporting Services)

Agora que já adicionou uma região de dados e alguns campos ao relatório de ordens de venda, você pode formatar os campos de data e moeda, além dos cabeçalhos da coluna.

## <a name="format-the-date"></a><a name="bkmk_format_date"></a>Formatar a data

Por padrão, a expressão Data exibe informações de data e hora. É possível formatá-lo para exibir apenas a data.

1. Selecione a guia **Design**.
2. Clique com o botão direito do mouse na célula com a expressão de campo `[Date]` e selecione **Propriedades da Caixa de Texto**.
3. Selecione o **Número** e, no campo **Categoria**, selecione a **Data**.
4. Na caixa **Tipo** , selecione **31 de janeiro de 2000**.
5. Selecione **OK** para aplicar o formato.
6. Visualize o relatório para ver a alteração na formatação do campo `[Date]` e, em seguida, retorne para a exibição de design.

## <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>Formatar a moeda

O campo Total da Linha exibe um número geral. É possível formatá-lo para exibir o número como moeda.

1. Clique com o botão direito do mouse na célula com a expressão `[LineTotal]` e selecione **Propriedades da Caixa de Texto**.
2. Selecione **Número**, na caixa de listagem da coluna à extrema esquerda, e **Moeda** na caixa de listagem **Categoria**.
3. Caso a configuração regional esteja em português (Brasil), os padrões na caixa de listagem **Tipo** devem ser:
    - **Casas decimais: 2**
    - **Números negativos: (R$ 1.2345,00)**
    - **Símbolo: R$ português (Brasil)**
4. Selecione **Usar separador de milhar (.)** . Caso o texto de exemplo seja **R$ 12.345,00**, as configurações estão corretas.
5. Selecione **OK** para aplicar o formato.
6. Visualize o relatório para ver a alteração na coluna da expressão `[LineTotal]` e depois retorne para a exibição de design.  

## <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>Alterar estilo do texto e larguras da coluna

Você pode adicionar outra formatação ao relatório, realce a linha de cabeçalho e ajuste as larguras das colunas de dados.

### <a name="to-format-header-rows-and-table-columns"></a>Para formatar as linhas do cabeçalho e as colunas da tabela

1. Selecione a tabela de forma que os identificadores de coluna e linha sejam exibidos acima e ao lado da tabela. As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.

2. Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste as colunas de acordo com o tamanho desejado.
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. Selecione a linha que contém rótulos de cabeçalho de coluna e, no menu **Formatar**, selecione **Fonte** > **Negrito**.

4. Visualize o relatório. Deve estar como mostrado a seguir:

    ![Visualização da tabela com cabeçalhos de colunas em negrito](media/rs-basictabledetailsformattedpreview.png "Visualização da tabela com cabeçalhos de colunas em negrito")  

5. No menu **Arquivo**, selecione **Salvar Tudo** para salvar o relatório.

## <a name="next-steps"></a>Próximas etapas

Nesta lição, você formatou com êxito os cabeçalhos de coluna e as expressões de campo. Agora você adicionará os agrupamentos e totais ao relatório. Continue com a [Lição 6: como adicionar agrupamentos e totais &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md).

## <a name="see-also"></a>Confira também

[Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
