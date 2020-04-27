---
title: Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10061"
- sql12.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f1f9750813d305834fe36f2c6ab7abfaa1d95075
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106765"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS)
  Adicione um retângulo a seu relatório quando quiser que um elemento gráfico separe áreas do relatório, enfatize áreas de um relatório ou forneça um plano de fundo para um ou mais itens de relatório. Os retângulos também são usados como contêineres para ajudar a controlar a maneira como as regiões de dados são renderizadas em um relatório. Você pode personalizar a aparência de um retângulo editando suas propriedades, como plano de fundo e cores da borda. Para obter mais informações sobre como usar um retângulo como um contêiner, consulte [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md) e [Exibir os mesmos dados em uma matriz e um gráfico &#40;Construtor de Relatórios&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
1.  Na guia **Inserir** , no grupo **Itens de Relatório** , clique em **Retângulo**.  
  
2.  Na superfície de design, clique no local onde deseja exibir o canto superior esquerdo do retângulo e arraste até onde deseja colocar o canto inferior direito.  
  
     À medida que você move o cursor, “linhas de ajuste” aparecem como as linhas do cursor junto com outros objetos na superfície de design. Isso será útil se você desejar alinhar os objetos.  
  
### <a name="to-create-a-container"></a>Para criar um contêiner  
  
1.  Adicione um item de relatório retângulo ao relatório.  
  
2.  Arraste outros itens de relatório para o retângulo.  
  
    > [!NOTE]  
    >  Um retângulo é um contêiner apenas para itens que você cria no retângulo ou arrasta para dentro dele. Se você desenhar um retângulo ao redor de um item que já existe na superfície de design, o retângulo não funcionará como seu contêiner.  
  
### <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>Para alterar propriedades de retângulo, como cor, estilo ou peso  
  
1.  Selecione o retângulo e clique nas opções de cor, estilo ou peso de linha na seção **Borda** da guia Página Inicial.  
  
2.  Clique na seta próxima ao botão **Borda** para determinar quais lados do retângulo devem ser alterados.  
  
    > [!NOTE]  
    >  Se você definir o estilo de linha como **duplo** e a largura da linha for de 1 1/2 pt ou mais estreita, a linha poderá não aparecer dupla quando você executar o relatório em Construtor de Relatórios, Report Designer ou Report Manager. Ela parecerá dupla quando você exportar o relatório para outros formatos, como Microsoft Word e Acrobat PDF.  
  
## <a name="see-also"></a>Consulte Também  
 [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)  
  
  
