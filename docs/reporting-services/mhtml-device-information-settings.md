---
title: Configurações de informações de dispositivo MHTML | Microsoft Docs
description: Saiba mais sobre as diversas configurações de informações de dispositivo para a renderização de relatórios no formato MHTML (Arquivo Web).
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a9570e0e7ddb85217e82e1813a67de84eee5a9c1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245549"
---
# <a name="mhtml-device-information-settings"></a>Configurações das informações do dispositivo MHTML
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios no arquivo da Web (MHTML).  
  
|Configuração|Valor|  
|-------------|-----------|  
|**JavaScript**|Indica se JavaScript é compatível com o relatório renderizado.|  
|**OutlookCompat**|Indica se ocorrerá renderização com metadados extras que melhoram a aparência do relatório no Outlook. O valor padrão é **true**.|  
|**Fragmento de MHTML**|Indica se um fragmento de MHTML é criado no lugar de um documento MHTML completo. Um fragmento de MHTML inclui o conteúdo do relatório em um elemento TABLE e omite os elementos HTML e BODY. O valor padrão é **false**.|  
|**DataVisualizationFitSizing**|Indica comportamento de ajuste de visualização de dados quando dentro de um tablix. Isso inclui gráfico, medidor e mapa.<br /><br /> Os valores possíveis são **Aproximado** e **Exato**.<br /><br /> O valor padrão é **Aproximado**. Se a configuração for removida do arquivo **rsreportserver.config** , o comportamento padrão será **Exato**.<br /><br /> Habilitar **Exato** pode ter impacto de desempenho porque o processamento para determinar o tamanho exato pode levar mais tempo.|  
  
## <a name="see-also"></a>Consulte Também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
