---
title: Configurações de informações de dispositivo PDF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 36def4705f6b2be9d5e1828f920ae41a51477272
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108093"
---
# <a name="pdf-device-information-settings"></a>Configurações de informações do dispositivo PDF
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios no formato PDF.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**Colunas**|O número de colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**ColumnSpacing**|O espaçamento entre colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**DpiX**|A resolução do dispositivo de saída em direção de x.|  
|**DpiY**|A resolução do dispositivo de saída em direção de y.|  
|**EndPage**|A última página do relatório a ser renderizado. O valor padrão é o valor de `StartPage`.|  
|`HumanReadablePDF`|Indica se o PDF deve ser compactado, permitindo que a origem fique mais legível. O valor padrão é `false.`|  
|**MarginBottom**|O valor da margem inferior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginLeft**|O valor da margem esquerda, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginRight**|O valor da margem direita, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginTop**|O valor da margem superior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**PageHeight**|A altura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 11in). Esse valor substitui as configurações originais do relatório.|  
|**PageWidth**|A largura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido por um "in" (por exemplo, 8,5in). Esse valor substitui as configurações originais do relatório.|  
|`StartPage`|A primeira página do relatório a ser renderizada. O valor `0` indica que todas as páginas serão renderizadas. O valor padrão é `1`.|  
  
## <a name="see-also"></a>Consulte Também  
 [Passando configurações de informações de dispositivo para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer. config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
