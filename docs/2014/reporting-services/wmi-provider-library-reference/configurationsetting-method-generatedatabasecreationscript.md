---
title: Método GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cf33e467e54fda5c29d81e3437730f0ce9547cad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098507"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserver_configurationsetting"></a>Método GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting)
  Gera um SQL Script que pode ser usado para criar um banco de dados do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>parâmetros  
 *Databasename*  
 Uma cadeia de caracteres que contém o nome do banco de dados do servidor de relatório a ser criado.  
  
 *Lcid*  
 O valor usado para localização de nomes de função.  
  
 *IsSharePointMode*  
 Indica se o banco de dados deve ser criado no modo nativo ou no modo do SharePoint.  
  
> [!IMPORTANT]  
>  A partir [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]do, o *issharepointmode* = `True` não tem suporte porque, no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint, é um serviço compartilhado do SharePoint e não é controlado pelo provedor WMI. Você sempre deve definir esse parâmetro como `False`.  
  
 *Script*  
 [fora] Uma cadeia de caracteres que contém o script SQL gerado.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Este método gera um script SQL que cria bancos de dados de servidor de relatório para a versão do servidor de relatório à qual está conectado.  
  
 O valor fornecido no parâmetro *DatabaseName* deve estar em conformidade com as convenções de nomenclatura de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O método não verifica se o banco de dados existe durante a geração do script.  
  
 Este método não verifica se o banco de dados do servidor de relatório existe durante a geração do script.  
  
 O script gerado dá suporte ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 e ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
