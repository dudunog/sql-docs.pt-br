---
title: Extensões do Reporting Services | Microsoft Docs
description: Saiba como estender as funcionalidades de processamento de dados no Reporting Services personalizando dados de relatório, mecanismos de notificação e sistemas de segurança.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 957b494e9bb581a8d41e0951cec62724e46c7d0d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524567"
---
# <a name="reporting-services-extensions"></a>Extensões do Reporting Services
  A arquitetura modular do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi desenhada para extensibilidade. Uma API de código gerenciado está disponível de forma que você possa desenvolver, instalar e gerenciar facilmente extensões consumidas por muitos componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você pode criar assemblies privados ou compartilhados usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e adicionar a nova funcionalidade do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para atender às suas necessidades empresariais em evolução.  
  
 A arquitetura de extensibilidade exclusiva do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] permite que os desenvolvedores estendam recursos específicos do produto e de seus componentes. Atualmente, existem um amplo suporte para a extensão dos recursos de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A API de processamento de dados construções de provedor de dados familiares do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e convenções que permitem aos desenvolvedores criarem processamento de dados adicional no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essas extensões de processamento de dados adicionam funcionalidade ao Servidor de Relatório e ao Designer de Relatórios, permitindo a integração direta de dados personalizados em relatórios.  
  
 Outra extensão com suporte é a extensão de entrega. A API de entrega é totalmente integrada à arquitetura do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], permitindo que uma ampla variedade de mecanismos de entrega seja usada no envio de notificações de relatório aos usuários. Você pode estender o Servidor de Relatório para fornecer entrega personalizada a usuários e pode estender as páginas de gerenciamento de assinatura do Gerenciador de Relatório para permitir que as assinaturas que usam extensões de entrega personalizadas.  
  
 Outra extensão de servidor de relatório, RDCE (Report Definition Customization Extension), pode personalizar uma definição de relatório dinamicamente antes de ser passada ao mecanismo de processamento. Você pode personalizar relatórios com base em fatores como usuários ou idiomas. Por exemplo, você poderia querer implementar exibições diferentes para vários usuários, como gerentes ou membros de um departamento, ou poderia querer personalizar um relatório para que ele tivesse um layout diferente quando renderizado em francês ou em árabe.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Considerações de segurança para extensões](../../reporting-services/extensions/security-considerations-for-extensions.md)  
 Descreve assuntos de segurança relacionados ao desenvolvimento e à implantação de extensões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)  
 Descreve os requisitos e as etapas de implementação de uma extensão de processamento de dados para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar uma extensão de entrega](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)  
 Descreve os requisitos e as etapas para a implementação de uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar uma extensão de renderização](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)  
 Contém uma introdução ao desenvolvimento de extensões de renderização.  
  
 [Implementando uma extensão de segurança](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
 Descreve os requisitos e as etapas para a implementação de uma extensão de segurança do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Biblioteca de extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extension-library.md)  
 Contém a referência de programação para a biblioteca de APIs de extensão para os recursos de extensibilidade do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
  
