---
title: Formatar um arquivo de script do Reporting Services | Microsoft Docs
description: Saiba como formatar um arquivo de script do Reporting Services no Microsoft Visual Basic .NET que contém procedimentos definidos pelo usuário e variáveis em nível de módulo.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], formats
- formats [Reporting Services], script files
ms.assetid: 85a207dd-4e0f-4d40-a41e-0c75f65d719c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1733a3f8a5e87086b696f81fec669229a443a275
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923382"
---
# <a name="format-a-reporting-services-script-file"></a>Formatar um arquivo de script do Reporting Services
  Um script [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é um arquivo de código [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET, escrito em um proxy criado em WSDL, que define a API SOAP do Reporting Services. Um arquivo de script é armazenado como arquivo de texto Unicode ou UTF-8 com extensão .rss.  
  
 O arquivo de script funciona como um módulo [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e pode conter procedimentos definidos pelo usuário e variáveis do nível de módulo. Para que o arquivo de script seja executado com êxito, ele deve conter um procedimento Main. O procedimento Main é o primeiro procedimento acessado quando o seu arquivo de script é executado. O Main é o local em que você pode acrescentar operações de serviço Web e executar subprocedimentos definidos pelo usuário. O código a seguir cria um procedimento Main:  
  
```  
Public Sub Main()  
    ' Your code goes here.  
End Sub  
```  
  
 O ambiente de script se conecta automaticamente ao servidor de relatório, cria a classe de proxy da Web e gera uma variável de referência (*rs*) para o objeto proxy de serviço Web. As instruções individuais que você cria precisam apenas fazer referência à variável do nível de módulo *rs* para realizar qualquer operação de serviço Web disponível na biblioteca de serviços Web. O código [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] a seguir chama o método de serviço Web <xref:ReportService2010.ReportingService2010.ListChildren%2A> do arquivo de script:  
  
```  
Public Sub Main()  
    Dim items() As CatalogItem  
    items = rs.ListChildren("/", True)  
  
    Dim item As CatalogItem  
    For Each item In items  
        Console.WriteLine(item.Name)  
    Next item  
End Sub   
```  
  
> [!IMPORTANT]  
>  As credenciais de usuário são administradas pelo ambiente de script e passadas pelos argumentos de prompt de comando pelo uso do RS.exe. Embora seja possível usar a variável *rs* para definir a autenticação do serviço Web, é recomendável que você utilize o ambiente de script. Não é necessário autenticar o serviço Web no próprio arquivo de script. Para obter mais informações sobre a autenticação do ambiente de script, consulte [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md).  
  
 Não declare namespaces dentro do arquivo de script. O ambiente de geração de scripts disponibiliza diversos namespaces úteis [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para você: **System.Web.Services**, **System.Web.Services.Protocols**, **System.Xml**e **System.IO**.  
  
 Para obter exemplos de script, consulte [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Web Servidor de Relatórios](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)  
  
  
