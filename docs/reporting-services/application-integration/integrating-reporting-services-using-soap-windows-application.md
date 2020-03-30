---
title: Usar a API SOAP em aplicativos do Windows
description: Você pode acessar a funcionalidade do servidor de relatório com a API SOAP do Reporting Services. Acesse o serviço Web em um aplicativo do Windows fazendo chamadas para o serviço.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
helpviewer_keywords:
- rendered reports [Reporting Services]
- Windows applications [Reporting Services]
- Windows Forms [Reporting Services]
- SOAP [Reporting Services], Windows applications
ms.assetid: e4804792-20cd-4df2-9257-fb958ff447b4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 78bdfb5335f00df64e1ae3a98a6a34aa26f71881
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198189"
---
# <a name="integrating-reporting-services-using-soap---windows-application"></a>Integrando o Reporting Services usando o SOAP – Aplicativo do Windows
  Você pode acessar a funcionalidade completa do servidor de relatório por meio da API SOAP do Reporting Services. A API SOAP é um serviço Web e, sendo assim, pode ser acessada facilmente para fornecer os recursos de relatórios corporativos para seus aplicativos comerciais personalizados. Você pode acessar o serviço Web em um aplicativo do Windows simplesmente gravando o código que faz chamadas para o serviço. Usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], é possível gerar uma classe proxy que expõe as propriedades e os métodos do serviço Web e permite que você use uma infraestrutura e ferramentas conhecidas para criar aplicativos de negócios baseados na tecnologia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="integrating-report-management-functionality-using-windows-forms"></a>Integrando a funcionalidade de gerenciamento de relatórios com o Windows Forms  
 Diferentemente do acesso de URL, a API SOAP expõe o conjunto completo de funções de gerenciamento disponíveis por meio do servidor de relatório. Isto significa que a funcionalidade administrativa inteira do Gerenciador de Relatórios está disponível para os desenvolvedores por meio de SOAP. Dessa forma, você pode desenvolver um gerenciamento completo e a ferramenta de administração usando o Windows Forms. Por exemplo, no aplicativo do Windows, você pode habilitar os usuários para recuperar o conteúdo do namespace do servidor de relatório. Para isso, você pode usar o método <xref:ReportService2010.ReportingService2010.ListChildren%2A> do serviço Web para listar todos os itens no banco de dados do servidor de relatório e, em seguida, usar um controle Listview, Treeview ou Combobox para exibir esses itens para os usuários. O código de serviço Web a seguir pode ser usado para recuperar a lista atual de relatórios disponíveis em uma pasta Meus Relatórios do usuário quando o usuário clica em um botão do formulário:  
  
```vb  
' Button click event that retrieves a list of reports from  
' the My Reports folder and displays them in a combo box  
Private Sub listReportsButton_Click(sender As Object, e As System.EventArgs)  
   ' Create a new Web service object and set credentials  
   ' to Windows Authentication  
   Dim rs As New ReportingService2010()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return the list of items in My Reports  
   Dim items As CatalogItem() = rs.ListChildren("/Adventureworks 2008 Sample Reports", False)  
  
   Dim ci As CatalogItem  
   For Each ci In  items  
      ' If the item is a report, add it to   
      ' a combo box  
      If ci.TypeName = "Report" Then  
         catalogComboBox.Items.Add(ci.Name)  
      End If  
   Next ci  
End Sub 'listReportsButton_Click  
```  
  
```csharp  
// Button click event that retrieves a list of reports from  
// the My Reports folder and displays them in a combo box  
private void listReportsButton_Click(object sender, System.EventArgs e)  
{  
   // Create a new Web service object and set credentials  
   // to Windows Authentication  
   ReportingService2010 rs = new ReportingService2010();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return the list of items in My Reports  
   CatalogItem[] items = rs.ListChildren("/Adventureworks 2008 Sample Reports", false);  
  
   foreach (CatalogItem ci in items)  
   {  
      // If the item is a report, add it to   
      // a combo box  
      if (ci.TypeName == "Report")  
         catalogComboBox.Items.Add(ci.Name);  
   }  
}  
```  
  
 A partir daí, você poderá habilitar os usuários para selecionar o relatório na caixa Combinação e visualizá-lo no formulário usando um controle do navegador da Web ou um controle de imagem.  
  
## <a name="enabling-report-viewing-and-navigation-using-windows-forms"></a>Habilitando a exibição e navegação do relatório por meio do Windows Forms  
 Há dois métodos disponíveis para integrar relatórios nos aplicativos do Windows Forms.  
  
 Você pode usar a API SOAP para renderizar relatórios em qualquer um dos formatos de renderização suportados usando o método <xref:ReportExecution2005.ReportExecutionService.Render%2A>. Há pequenas desvantagens em habilitar a exibição e navegação de relatório por meio de SOAP:  
  
-   Você não pode se beneficiar da funcionalidade interna da barra de ferramentas do relatório que é incluída com o Visualizador de HTML por meio do acesso de URL.  
  
-   Se você renderizar para HTML, deverá renderizar separadamente quaisquer imagem ou recursos como fluxos adicionais que usam o método <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A>.  
  
-   Há uma pequena vantagem de desempenho na renderização de relatórios com o acesso de URL em relação à API SOAP.  
  
 Porém, o método <xref:ReportExecution2005.ReportExecutionService.Render%2A> da API SOAP pode ser usado para renderizar relatórios e salvá-los em vários formatos de saída programaticamente. Essa é uma vantagem em relação ao acesso de URL que requer interação de usuário. Quando você renderizar um relatório que usa o método <xref:ReportExecution2005.ReportExecutionService.Render%2A> de SOAP API, será possível renderizar em qualquer um dos formatos de saída suportados.  
  
 Você também pode usar os controles do Visualizador de Relatórios que são distribuídos gratuitamente e estão incluídos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]. Os controles do Visualizador de Relatórios facilitam a inserção da funcionalidade [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em aplicativos personalizados. Os controles d Visualizador de Relatórios são destinados a desenvolvedores que desejam fornecer relatórios com design prévio, totalmente criados como parte de um conjunto de recursos do aplicativo (por exemplo, um aplicativo de gerenciamento de site da Web pode incluir relatórios que mostrem a análise de fluxo de acesso a sites da Web da empresa). A inserção de controles em um aplicativo fornece uma alternativa otimizada para incluir os componentes de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em sua implantação de aplicativo. Os controles fornecem a funcionalidade de relatório, mas sem a criação de relatório adicional, publicação ou distribuição e suporte de entrega que você localiza no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Há duas versões de controles do Visualizador de Relatórios, uma para aplicativos cliente sofisticados do Windows e uma para aplicativos [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Os controles dão suporte ao processamento local e aos modos de processamento remotos. No modo de processamento local, o aplicativo fornece a definição de relatório e conjuntos de dados, e dispara o processamento do relatório. No modo de processamento remoto, a recuperação de dados e o processando de relatório ocorre no servidor de relatório e o controle é usado para exibição e navegação no relatório. Esse modelo permite que você crie aplicativos sofisticados que podem ser escalados da área de trabalho à empresa.  
  
 Os controles do Visualizador de Relatórios são documentados na Ajuda online do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para obter mais informações, consulte a documentação do produto do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Usando a API SOAP em um aplicativo Web](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
  
  
