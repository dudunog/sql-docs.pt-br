---
description: Propriedade DatabaseQueryTimeout (WMI MSReportServer_ConfigurationSetting)
title: Propriedade DatabaseQueryTimeout (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5772326704b5e5fd6861b6185dab75cefdf42d1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472628"
---
# <a name="configurationsetting-property---databasequerytimeout"></a>Propriedade de ConfigurationSetting – DatabaseQueryTimeout
  Especifica o número de segundos que devem decorrer antes de o servidor de relatório assumir que o comando falhou ou demorou demais para executar. O servidor de relatório está cronometrando a consulta no catálogo de SQL, não uma fonte de dados para o relatório. Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **inteiro** sem sinal de 32 bits que representa o número de segundos que a consulta tem permissão para executar.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
