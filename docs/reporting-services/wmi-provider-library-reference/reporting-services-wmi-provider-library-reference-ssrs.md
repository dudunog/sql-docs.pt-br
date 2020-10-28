---
description: Referência da Biblioteca do provedor WMI do Reporting Services (SSRS)
title: Referência da biblioteca do provedor WMI do Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 88c12fdc3748b89ad3daba6fcdf5fcd22cdabaf9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "92255561"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Referência da Biblioteca do provedor WMI do Reporting Services (SSRS)
  O provedor WMI (Instrumentação de Gerenciamento do Windows) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte às operações do WMI que permitem gravar scripts e código para modificar as configurações do servidor de relatório e do Gerenciador de Relatórios.  
  
 Por exemplo, se você quiser alterar quando a segurança integrada é usada quando o servidor de relatório se conecta ao banco de dados do servidor de relatório, crie uma instância da classe MSReportServer_ConfigurationSetting e use a propriedade DatabaseIntegratedSecurity da instância do servidor de relatório. As classes mostradas na tabela a seguir representam os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As classes são definidas nos namespaces do [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] ou do [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] . Cada uma das classes oferece suporte às operações de leitura e gravação. As operações de criação não têm suporte.  
  
## <a name="classes"></a>Classes  
 [Classe MSReportServer_Instance](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 Fornece as informações básicas exigidas para um cliente se conectar a um servidor de relatório instalado.  
  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 Representa os parâmetros de instalação e de tempo de execução de uma instância do servidor de relatório. Esses parâmetros são armazenados no arquivo de configuração para o servidor de relatório.  
  
 Para obter mais informações sobre as operações WMI, confira a documentação do SDK do WMI incluída no SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar o provedor WMI do Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
