---
title: Adicionar parâmetros a um relatório móvel | Reporting Services | Microsoft Docs
description: O relatório móvel do Reporting Services pode ter parâmetros, portanto, os leitores de relatório podem filtrar seus relatórios. Esse relatório também pode ser o destino de um detalhamento.
ms.date: 07/30/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41895890a5528a1ddac90a4c9f9eea05d80fac93
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448297"
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>Adicionar parâmetros a um relatório móvel | Reporting Services
Você pode criar um relatório móvel do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com parâmetros, para que você e os leitores do relatório possam filtrar seus relatórios. Um relatório com parâmetros também pode ser o destino de um [detalhamento de um relatório de origem](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md). 

Para criar um relatório móvel com parâmetros, comece com um conjunto de dados compartilhado com, pelo menos, um parâmetro. Leia sobre [como criar parâmetros em um conjunto de dados compartilhado](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md). Os relatórios móveis não oferecem suporte a valores nulos para os parâmetros padrão, portanto, certifique-se de que os parâmetros têm valores padrão diferentes de nulo.

Depois de adicionar parâmetros a um relatório móvel, você cria uma URL para [abrir o relatório com parâmetros de cadeia de consulta](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md). 

1. Na barra superior do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] , selecione **Novo** > **Relatório Móvel**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Selecione a guia **Dados** no canto superior esquerdo do [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)].   
  
3. No canto superior direito, selecione **Adicionar Dados**.  
  
4. Selecione **Servidor de Relatório**e um servidor.  
  
5. Navegue até os conjuntos de dados compartilhados no servidor e escolha um que têm parâmetros.  
  
   Na grade, você vê os dados no conjunto de dados. O círculo verde com colchetes **{}** marca um conjunto de dados com um parâmetro.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. Selecione a engrenagem na guia **Param {}** .  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. Selecione o elemento de relatório que passará valores para o parâmetro.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. Selecione **Visualização** para ver a aparência do relatório. Neste relatório, a lista de seleção usa o parâmetro Category.

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. Quando você seleciona um valor na lista de seleção, o relatório é filtrado para esse valor, nesse caso, Acessórios.

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>Confira também  
-  [Abrir um relatório móvel com parâmetros de cadeia de caracteres de consulta específicos](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [Adicionar o detalhamento de um relatório móvel para outros relatórios móveis ou URLs](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [Criar um conjunto de dados compartilhado ou inserido](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

