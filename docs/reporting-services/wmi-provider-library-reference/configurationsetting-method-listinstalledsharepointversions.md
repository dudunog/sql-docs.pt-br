---
description: Método de ConfigurationSetting – ListInstalledSharePointVersions
title: Método ListInstalledSharePointVersions (WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3305eb8e802dbebc39960105813a58ea16ab3055
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480668"
---
# <a name="configurationsetting-method---listinstalledsharepointversions"></a>Método de ConfigurationSetting – ListInstalledSharePointVersions
  Retorna um conjunto de tokens que representam as versões do Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)][!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *VersionTokens[]*  
 [fora] Uma matriz que contém os tokens que representam a versão de um produto do SharePoint ou tecnologia que é compatível com o servidor de relatório instalado.  
  
 *Comprimento*  
 [fora] O tamanho da matriz de tokens da versão.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Cada token retornado representa uma versão do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] ou [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] que é compatível com o servidor de relatório atualmente instalado. Se uma versão específica do SharePoint for compatível com versões anteriores do SharePoint, serão retornados tokens de cada versão compatível do SharePoint.  
  
 A seguir é apresentada uma tabela dos tokens do SharePoint que são retornados.  
  
|**Tokens da versão**|**Descrição**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|É executada uma instalação do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] , que é compatível com o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0.|  
|WSS_V3_Compatible|É executada uma instalação do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que é compatível com o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0.|  
|WSS_V4_Compatible|É executada uma instalação do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que é compatível com o Office 14.|  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
