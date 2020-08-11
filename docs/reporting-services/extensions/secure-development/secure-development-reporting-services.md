---
title: Desenvolvimento seguro (Reporting Services) | Microsoft Docs
description: Saiba mais sobre o sistema de segurança de acesso do código que o Reporting Services usa, que executa o código em contextos de segurança restritos e definidos pelo administrador.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 69d60e4a68deee28c639cc5e100456ef1c9c3552
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529396"
---
# <a name="secure-development-reporting-services"></a>Desenvolvimento seguro (Reporting Services)
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornece um sistema de segurança robusto que pode executar o código em contextos de segurança altamente restritos definidos pelo administrador. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa o sistema de segurança do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], conhecido como segurança de acesso a código (ou segurança baseada em evidência). Na segurança de acesso do código, um usuário pode ser confiável para acessar um recurso, mas se o código executado pelo usuário não for confiável, o acesso ao recurso será negado.  
  
 A segurança baseada em código, ao contrário de usuários específicos, permite que a segurança seja expressa para assemblies ou dados personalizados, entrega, criação e extensões de segurança desenvolvidos para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O código de extensão pode ser executado por qualquer número de usuários do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], todos conhecidos durante o desenvolvimento. Os assemblies ou extensões personalizados que você desenvolve exigem políticas de segurança específicas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Essas políticas de segurança são representadas como tipos no [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre segurança de acesso do código, consulte "Segurança de acesso do código" na documentação do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Segurança de acesso do código no Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)  
 Apresenta a segurança de acesso do código e a configuração de políticas para extensões e assemblies personalizados no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Compreender as políticas de segurança](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
 Descreve os vários tipos de assembly no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e como a segurança de acesso do código afeta permissões de código.  
  
 [Usar arquivos de política de segurança do Reporting Services](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)  
 Descreve os diferentes componentes do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e os arquivos de configuração de política correspondentes.  
  
  
