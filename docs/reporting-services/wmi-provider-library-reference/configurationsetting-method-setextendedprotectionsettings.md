---
description: Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting)
title: Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 80693f5720974bedc8c0d4dae13ed4bb24727980
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480638"
---
# <a name="configurationsetting-method---setextendedprotectionsettings"></a>Método de ConfigurationSetting – SetExtendedProtectionSettings
  O método SetExtendedProtectionSettings é usado para definir as propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario no arquivo de configuração RSReportServer.config do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ExtendedProtectionLevel*  
 Define o RSWindowsExtendedProtectionLevel no arquivo RSRreportserver.config. O valor obrigatório não diferencia maiúsculas de minúsculas.  
  
 A lista a seguir mostra os valores válidos:  
  
 `"Off | Allow | Require"`  
  
 *ExtendedProtectionScenario*  
 Define o RSWindowsExtendedProtectionScenario no arquivo RSReportserver.config. O valor obrigatório não diferencia maiúsculas de minúsculas.  
  
 A lista a seguir mostra os valores válidos:  
  
 `"Any" | "Proxy" | "Direct"`  
  
## <a name="remarks"></a>Comentários  
 As propriedades RSWindowsExtendedProtectionLevel e RSWindowsExtendedProtectionScenario aplicam-se quando AuthenticationTypes no arquivo RSReportServer.config inclui RSWindowNTLM, RSWindowsNegotiate ou RSWindowsKerberos. Definir essas propriedades afeta a maneira como os usuários e o software cliente se autenticam com um servidor de relatórios. É recomendável ler a documentação da proteção estendida antes de definir ExtendedProtectionLevel como **Allow** ou **Require**.  
  
 Para definir o ExtendedProtectionLevel, o usuário deve ser membro do grupo BUILTIN\Administradores no servidor de relatório.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade RSWindowsExtendedProtectionScenario &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [Propriedade RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Proteção Estendida para Autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
