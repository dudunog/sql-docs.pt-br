---
title: Alterar um item de uma célula (Construtor de Relatórios) | Microsoft Docs
description: Substitua um item não contêiner, como uma caixa de texto, linha ou imagem, em relatórios paginados com um novo item de relatório no Construtor de Relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91a54778-8929-41f9-bb4c-826cec636be4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c262d1c3b84f65c80897c28e6fa4de826aeb3a30
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255639"
---
# <a name="change-an-item-within-a-cell-report-builder-and-ssrs"></a>Alterar um item de uma célula (Construtor de Relatórios e SSRS)
Em relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , somente um item não contêiner, como uma caixa de texto, linha ou imagem, pode ser substituído por um novo item de relatório. Por exemplo, é possível arrastar uma tabela para uma caixa de texto a fim de substituí-la pela tabela.  
  
 Se a célula contiver um item de contêiner, como um retângulo, lista, tabela ou matriz, o novo item será adicionado a ele em vez de substituí-lo. Para substituir um item por um novo item, exclua o contêiner. A exclusão do contêiner substitui o mesmo por uma caixa de texto, que você pode então substituir por outro item.  
  
 Por padrão, todas as células de uma tabela, matriz ou região de dados da lista contêm uma caixa de texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-an-item-within-a-cell"></a>Para alterar um item de uma célula  
  
-   Na guia **Inserir** , no grupo **Regiões de Dados** ou **Itens de Relatório** , clique no item que você deseja adicionar ao relatório e, em seguida, clique no relatório. O item será adicionado ao relatório.  
  
> [!NOTE]  
>  A caixa de diálogo **Propriedades da Imagem** é aberta quando você arrasta um item de relatório de imagem para uma célula, na qual é possível definir propriedades, como a origem da imagem, antes de adicionar a imagem à célula.  
  
## <a name="see-also"></a>Consulte Também  
 [Imagens, caixas de texto, retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
