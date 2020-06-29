---
title: Gerenciar funções de pacote programaticamente (Serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: dff54f3f90d9e008ae21c83c2a8fdc3f7440a5c3
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422703"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Gerenciando funções de pacote programaticamente (Serviço SSIS)
  Ao trabalhar programaticamente com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], talvez você queira determinar quais funções estão disponíveis para aplicar a pacotes ou determinar/definir as funções aplicadas a um único pacote. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.

 As funções se aplicam apenas aos pacotes armazenados no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]msdb**do**. Para obter mais informações sobre funções de pacote, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../security/integration-services-roles-ssis-service.md).

 Todos os métodos discutidos neste tópico exigem uma referência ao assembly `Microsoft.SqlServer.ManagedDTS`. Depois de adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> através de uma instrução `using` ou `Imports`.

> [!IMPORTANT]
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".

## <a name="determining-which-roles-are-available"></a>Determinando quais funções estão disponíveis
 Para determinar quais funções estão disponíveis para os pacotes armazenados em um servidor específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application>.

## <a name="determining-which-roles-are-assigned"></a>Determinando quais funções são atribuídas
 Para determinar quais funções já foram atribuídas a um pacote específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para atribuir funções a um pacote, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.

![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [Funções do Integration Services &#40;SSIS Service&#41;](../security/integration-services-roles-ssis-service.md)


