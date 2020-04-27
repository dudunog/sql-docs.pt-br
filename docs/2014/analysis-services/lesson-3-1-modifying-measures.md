---
title: Modificando medidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 663ef21dc9c4d0f3698ae468637fe0a8fd55a16e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078896"
---
# <a name="modifying-measures"></a>Modificando medidas
  Você pode usar a propriedade **FormatString** para definir configurações de formatação que controlam como as medidas são exibidas aos usuários. Nesta tarefa, você especificará propriedades de formatação para as medidas moeda e porcentagem do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### <a name="to-modify-the-measures-of-the-cube"></a>Para modificar as medidas do cubo  
  
1.  Mude para a guia **Estrutura do Cubo** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , expanda o grupo de medidas **Vendas pela Internet** no painel **Medidas** , clique com o botão direito do mouse em **Quantidade de Pedidos**e clique em **Propriedades**.  
  
2.  Na janela Propriedades, clique no ícone de pino **Ocultar Automaticamente** para manter a janela Propriedades aberta.  
  
     É mais fácil alterar as propriedades de vários itens no cubo quando a janela Propriedades permanece aberta.  
  
3.  Na janela Propriedades, clique na lista **FormatString** e digite **#,#**.  
  
4.  Na barra de ferramentas da guia **Estrutura do Cubo** , clique no ícone **Mostrar Grade de Medidas** à esquerda.  
  
     A exibição das grades permite que você selecione várias medidas ao mesmo tempo.  
  
5.  Selecione as medidas a seguir. Você pode selecionar várias medidas clicando em cada uma enquanto mantém pressionada a tecla CTRL.  
  
    -   **Preço Unitário**  
  
    -   **Valor Ampliado**  
  
    -   **Valor de desconto**  
  
    -   **Custo Padrão do Produto**  
  
    -   **Custo Total do Produto**  
  
    -   **Valor das Vendas**  
  
    -   **Valor dos Impostos**  
  
    -   **Freight**  
  
6.  Na janela Propriedades, na lista **FormatString** , selecione **Moeda**.  
  
7.  Na lista suspensa na parte superior da janela Propriedades (logo abaixo da barra de título), selecione a medida **Percentual de Desconto no Preço Unitário**e **Percentual** na lista **FormatString** .  
  
8.  No janela Propriedades, altere a propriedade **nome** da medida **percentual de desconto de preço unitário** para `Unit Price Discount Percentage`.  
  
9. No painel **medidas** , clique em **imposto AMT** e altere o nome dessa medida para `Tax Amount`.  
  
10. Na janela Propriedades, clique no ícone **Ocultar Automaticamente** para ocultar a janela Propriedades. Depois, clique em **Mostrar Árvore de Medidas** na barra de ferramentas da guia **Estrutura do Cubo** .  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando a dimensão Cliente](lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Definir dimensões de banco de dados](multidimensional-models/define-database-dimensions.md)   
 [Configurar propriedades de medida](multidimensional-models/configure-measure-properties.md)  
  
  
