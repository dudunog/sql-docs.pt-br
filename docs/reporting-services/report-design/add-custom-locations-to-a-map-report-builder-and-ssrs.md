---
title: Adicionar locais personalizados a um mapa (Construtor de Relatórios) | Microsoft Docs
description: Saiba como adicionar locais personalizados a um mapa que você adicionou a um relatório paginado no Construtor de Relatórios.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf6610f1abb446d27825e8d2e95677100a69184d
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255669"
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>Adicionar locais personalizados a um mapa (Construtor de Relatórios e SSRS)
  Depois que adicionar um mapa a um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , você poderá adicionar seus próprios locais de ponto.  
  
 As propriedades de exibição de todos os pontos em uma camada são controladas pela definição de opções para as propriedades de ponto da camada. Para um ponto inserido selecionado, você pode substituir as propriedades de exibição.  
  
> [!NOTE]  
>  Quando você substituir as propriedades de exibição da camada para o ponto inserido, as alterações feitas não serão reversíveis.  
  
 Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-point-layer"></a>Para adicionar uma camada de ponto  
  
1.  Na superfície de design de relatório, clique no mapa para selecioná-lo e exibir o painel Mapa.  
  
2.  Na barra de ferramentas, clique em **Adicionar Camada**.  
  
3.  Na lista suspensa, clique em **Adicionar Camada de Ponto**. Uma camada de ponto sem pontos é adicionada ao mapa. Por padrão, a camada de ponto está pronta para pontos inseridos.  
  
## <a name="to-add-a-custom-point"></a>Para adicionar um ponto personalizado  
  
1.  Na superfície de design de relatório, clique no mapa para selecioná-lo e exibir o painel Mapa.  
  
2.  No painel Mapa, clique com o botão direito do mouse em uma camada de ponto que tenha o tipo **Inserido**e clique em **Adicionar Ponto**. O cursor se transforma em uma cruz.  
  
3.  Para adicionar um ponto, clique em um local no mapa. Um ponto inserido é adicionado à camada selecionada no local em que você clica.  
  
## <a name="to-customize-the-display-for-an-embedded-point"></a>Para personalizar a exibição para um ponto inserido  
  
1.  Clique com o botão direito do mouse no ponto e clique em **Propriedades de Ponto**. A caixa de diálogo **Propriedades do Ponto Inserido do Mapa** aparece.  
  
2.  Clique em **Substituir opções de ponto para esta camada**. Várias páginas de propriedades aparecem no painel esquerdo.  
  
3.  Clique nas páginas e defina as propriedades de exibição que você deseja aplicar a esse ponto.  
  
## <a name="see-also"></a>Consulte Também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
