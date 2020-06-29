---
title: Gerenciar pacotes em execução programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2ffaeac67c91c520ba657b96afc97898328a8299
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422633"
---
# <a name="managing-running-packages-programmatically"></a>Gerenciando pacotes em execução programaticamente
  Ao trabalhar programaticamente com pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], determine quais pacotes estão em execução no momento. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos e classes que atendem a esses requisitos.  
  
 Para obter mais informações sobre o monitoramento de pacotes, consulte [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../service/package-management-ssis-service.md).  
  
 Todos os métodos discutidos neste tópico exigem uma referência ao assembly `Microsoft.SqlServer.ManagedDTS`. Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> com uma instrução `using` ou `Imports`.  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
## <a name="determining-which-packages-are-currently-running"></a>Determinando quais pacotes estão em execução atualmente  
 Para determinar quais pacotes estão em execução atualmente no servidor especificado, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Esse método retorna uma coleção <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> de objetos <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Administradores consultam todos os pacotes que estão em execução atualmente no computador; outros usuários só verificam os pacotes iniciados por eles.  
  
## <a name="working-with-running-packages"></a>Trabalhando com pacotes em execução  
 Depois de determinar quais pacotes estão em execução no momento, você poderá recuperar informações sobre os pacotes e solicitar que um pacote seja interrompido.  
  
### <a name="getting-information-about-a-running-package"></a>Obtendo informações sobre um pacote em execução  
 Ao iterar na coleção <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages>, você pode utilizar as propriedades do objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para localizar um pacote ou para obter informações adicionais sobre os pacotes em execução:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Interrompendo um pacote em execução  
 Você pode chamar o método <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> de um objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para solicitar que o pacote seja interrompido. Pode haver um atraso entre a hora em que uma solicitação de interrupção é emitida e a hora em que o pacote é realmente interrompido.  
  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de Pacotes &#40;serviço SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerando pacotes disponíveis programaticamente](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
