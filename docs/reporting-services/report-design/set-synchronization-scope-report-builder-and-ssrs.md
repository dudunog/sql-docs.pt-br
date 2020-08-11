---
title: Definir o escopo de sincronização (Construtor de Relatórios) | Microsoft Docs
description: Defina o escopo de sincronização em um relatório paginado com indicadores para transmitir valores de dados fazendo a sincronização do intervalo de valores de indicador no Construtor de Relatórios.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ff29909da8662d39cadb064bab66eb14df9d013
ms.sourcegitcommit: f898aa83561e94626024916932568ab05e73b656
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/27/2020
ms.locfileid: "84012589"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>Definir o escopo da sincronização (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , os indicadores transmitem valores de dados fazendo a sincronização do intervalo de valores de dados de indicador em um escopo especificado.   
    
  Por padrão, o escopo é o contêiner pai do indicador, como a tabela ou matriz que contém o indicador. Você pode alterar a sincronização do indicador dependendo do layout do seu relatório. Por exemplo, se uma região de dados, como uma tabela, tiver um grupo de linhas, você poderá especificar o grupo como o escopo de indicador. O indicador também pode omitir a sincronização.  
  
 Opções como unidades de medida podem ser definidas usando expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Para obter informações gerais sobre como entender e definir escopo em relatórios, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="to-change-the-synchronization-scope-of-an-indicator"></a>Para alterar o escopo da sincronização de um indicador  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Na lista **Escopo da sincronização** , clique no escopo que você deseja aplicar.  
  
     A opção **(Nenhum)** , que remove o escopo da sincronização do indicador, está sempre disponível. Outras opções dependem do layout do relatório.  
  
     Se desejar, clique no botão **Expressão** (*fx*) para editar uma expressão que define o escopo.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
