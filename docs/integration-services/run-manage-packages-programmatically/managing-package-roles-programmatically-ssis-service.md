---
title: Gerenciar funções de pacote programaticamente (Serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ca7748f3a768edf438fa2da1b4db836bbde2012
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913305"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Gerenciando funções de pacote programaticamente (Serviço SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Ao trabalhar programaticamente com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], talvez você queira determinar quais funções estão disponíveis para aplicar a pacotes ou determinar/definir as funções aplicadas a um único pacote. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.  
  
 As funções se aplicam apenas aos pacotes armazenados no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]msdb**do**. Para obter mais informações sobre funções de pacote, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos os métodos discutidos neste tópico exigem uma referência ao assembly **Microsoft.SqlServer.ManagedDTS**. Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> usando uma instrução **using** ou **Imports**.  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinando quais funções estão disponíveis  
 Para determinar quais funções estão disponíveis para os pacotes armazenados em um servidor específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinando quais funções são atribuídas  
 Para determinar quais funções já foram atribuídas a um pacote específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para atribuir funções a um pacote, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções do Integration Services &#40;SSIS Service&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
