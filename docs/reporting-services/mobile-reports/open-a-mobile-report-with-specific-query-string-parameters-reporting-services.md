---
title: Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Microsoft Docs
description: Para um relatório móvel do Reporting Services com parâmetros e uma fonte de dados, você pode usar parâmetros de consulta na URL do relatório para abri-lo com valores especificados.
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: abcdda5a396451508df78610eeb4f7bc417484d5
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907344"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Reporting Services
Se você tiver um relatório móvel [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com parâmetros e uma fonte de dados [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)], poderá incluir parâmetros de cadeia de consulta na URL do relatório para que abra automaticamente com os valores especificados. 
1.  Crie um [relatório móvel com parâmetros](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Abra o relatório no Publicador de Relatórios Móveis e selecione a guia Dados. 

2. Encontre o nome do conjunto de dados na guia, na parte inferior da tabela, e o nome do campo desejado. 
    
    ![Captura de tela da exibição dos dados de parâmetros do editor de relatórios móveis.](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  A sintaxe da URL depende de sua fonte de dados. 

     **Para uma fonte de dados do SQL Server Analysis Services** : Crie uma URL com um parâmetro de cadeia de consulta neste formato:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Por exemplo:
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Para uma fonte de dados do SQL Server** : o parâmetro de cadeia de caracteres de consulta é praticamente o mesmo, mas tem o símbolo \@ na frente do nome do campo:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Por exemplo:
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Essa URL abrirá o relatório no servidor, automaticamente filtrado para o valor de parâmetro especificado.

    ![Captura de tela da exibição do portal da Web de parâmetros do editor de relatórios móveis com uma seta apontando para a URL e uma caixa ao redor do texto: ?TimeChartLoD.@category=Clothing.](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Confira também

[Adicionar parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

