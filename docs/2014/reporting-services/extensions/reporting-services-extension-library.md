---
title: Biblioteca de extensões do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d09464ce4a61903a3e9b74711482d2ce07bd0c4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62985748"
---
# <a name="reporting-services-extension-library"></a>Biblioteca de extensões do Reporting Services
  A biblioteca de extensões do Reporting Services é um conjunto de classes, interfaces e tipos de valores que são incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa biblioteca fornece acesso à funcionalidade do sistema e foi projetada para ser a base sobre a qual os aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] podem ser usados para estender os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="namespaces"></a>Namespaces  
 A biblioteca de extensão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece os namespaces a seguir.  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 Contém classes e interfaces que permitem a criação de componentes que estendem a capacidade do processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 Contém classes e interfaces que permitem a criação e o envio de notificações personalizadas para usuários por meio de suas próprias extensões de entrega e a criação de extensões de segurança personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 `Microsoft.ReportingServices.ReportRendering`  
 Contém classes e interfaces que permitem a extensão dos recursos de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Usando os membros desse namespace junto com os membros do namespace <xref:Microsoft.ReportingServices.Interfaces>, você pode criar suas próprias extensões de renderização personalizadas para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](reporting-services-extensions.md)  
  
  
