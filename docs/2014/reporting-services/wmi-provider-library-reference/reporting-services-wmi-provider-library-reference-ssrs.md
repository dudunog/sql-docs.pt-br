---
title: Referência da biblioteca do provedor WMI do Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider Library
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a98ca22f9d34627e484a698dcf540b31808d07e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097018"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Referência da Biblioteca do provedor WMI do Reporting Services (SSRS)
  O provedor WMI (Instrumentação de Gerenciamento do Windows) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte às operações do WMI que permitem gravar scripts e código para modificar as configurações do servidor de relatório e do Gerenciador de Relatórios.  
  
 Por exemplo, se você quiser alterar quando a segurança integrada é usada quando o servidor de relatório se conecta ao banco de dados do servidor de relatório, crie uma instância da classe MSReportServer_ConfigurationSetting e use a propriedade DatabaseIntegratedSecurity da instância do servidor de relatório. As classes mostradas na tabela a seguir representam os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As classes são definidas nos namespaces do [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] ou do [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] . Cada uma das classes oferece suporte às operações de leitura e gravação. As operações de criação não têm suporte.  
  
## <a name="classes"></a>Classes  
 [Classe MSReportServer_Instance](msreportserver-instance-class.md)  
 Fornece as informações básicas exigidas para um cliente se conectar a um servidor de relatório instalado.  
  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
 Representa os parâmetros de instalação e de tempo de execução de uma instância do servidor de relatório. Esses parâmetros são armazenados no arquivo de configuração para o servidor de relatório.  
  
 Para obter mais informações sobre as operações do WMI, consulte a documentação do SDK [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] do WMI incluída no SDK.  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar o provedor WMI de Reporting Services](../tools/access-the-reporting-services-wmi-provider.md)   
 [Referência técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
