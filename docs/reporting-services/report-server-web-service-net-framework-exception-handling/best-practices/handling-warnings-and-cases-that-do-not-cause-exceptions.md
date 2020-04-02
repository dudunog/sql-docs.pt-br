---
title: Manipulando avisos e casos que não causam exceções | Microsoft Docs
description: Saiba como lidar com avisos e casos que não causam exceções para que a medida correta possa ser adotada.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], warnings that don't cause
- warnings [Reporting Services]
ms.assetid: 475c0713-6265-44e7-9ebc-ebdd1b89e0af
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5dd1c9335db348aeb3cb979079d3f1bd929f008a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216385"
---
# <a name="handling-warnings-and-cases-that-do-not-cause-exceptions"></a>Manipulando avisos e casos que não causam exceções
  O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não lança exceções para avisos e para certos erros. Por exemplo, quando você usa o método <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> para publicar um novo relatório em um servidor de relatório, qualquer aviso que ocorrer será retornado como uma matriz de objetos de <xref:ReportService2010.Warning>. Esses avisos devem ser manipulados e exibidos para que a ação apropriada seja tomada.  
  
```vb  
Try  
   rs.CreateCatalogItem(name, parentFolder, False, definition, Nothing, warnings)  
  
   If Not (warnings.Length = 0) Then  
      Dim warning As Warning  
      For Each warning In warnings  
         Console.WriteLine(warning.Message)  
      Next warning  
   Else  
      Console.WriteLine("Report {0} created successfully with no warnings", name)  
   End If  
  
Catch ex As SoapException  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.CreateCatalogItem("Report", name, parentFolder, false, definition, null, out warnings);  
  
   if (warnings.Length != 0)  
   {  
      foreach (Warning warning in warnings)  
      {  
         Console.WriteLine(warning.Message);  
      }  
   }  
   else  
      Console.WriteLine("Report {0} created successfully with no warnings", name);  
}  
  
catch (SoapException ex)  
{  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
 Outro modo de manipular erros é avaliando os valores retornados de certos métodos. Por exemplo, o método de <xref:ReportService2010.ReportingService2010.FindItems%2A> pode ser usado para procurar itens específicos no banco de dados do servidor de relatório. Se não for localizado nenhum item que corresponda aos critérios de pesquisa, será retornada uma matriz nula de objetos de <xref:ReportService2010.CatalogItem>. Avalie a matriz, verifique a existência de **null** e avise o usuário caso nenhum item tenha sido encontrado.  
  
## <a name="see-also"></a>Consulte Também  
 <xref:ReportService2010.CatalogItem>   
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services +](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
