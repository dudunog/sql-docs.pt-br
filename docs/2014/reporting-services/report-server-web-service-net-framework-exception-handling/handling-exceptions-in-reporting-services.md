---
title: Tratando exceções no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1d887853b475f7b4d673d7b04343ae9bc71644d3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046038"
---
# <a name="handling-exceptions-in-reporting-services"></a>Manipulando exceções no Reporting Services
  Quando uma solicitação de cliente API SOAP do Reporting Services não pode ser concluída, o servidor de relatório retorna um erro em vez dos resultados esperados da chamada. Quando uma chamada não pode ser concluída, é retornado um erro para o serviço Web Servidor de Relatórios como um elemento XML **Falha** de SOAP. O principal elemento descritivo da falha é o elemento **detail**, que inclui todas as informações de erro fornecidas pelo servidor de relatório, além de informações adicionais de erro do serviço Web. A principal informação do elemento **detail** é o código de erro do servidor de relatório. com base na mensagem e no código de erro, você poderá determinar a próxima ação apropriada a ser tomada levar em seus aplicativos. Para saber mais sobre falhas SOAP, veja o site do W3C (World Wide Web Consortium), http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>As falhas SOAP e o .NET Framework  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], se houver um erro em uma solicitação de cliente feita a um serviço Web, o servidor de relatório comunicará o erro ao código do cliente que chama o serviço Web gerando um objeto **SoapException**. **SoapException** encapsula a informações contidas em uma falha de SOAP. A propriedade **Detail** de **SoapException** é mapeada para o elemento **detail** na falha de SOAP. Os aplicativos devem capturar o objeto **SoapException** com um bloco try/catch e usar a propriedade **Detail** de **SoapException** para tomar a ação apropriada. Para obter mais informações sobre a classe **SoapException** e a propriedade **Detail** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Classe SoapException do Reporting Services](soapexception-class/reporting-services-soapexception-class.md). Para obter mais informações sobre a classe **SoapException**, confira a documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Detail](soapexception-class/detail-property.md)   
 [Introdução à manipulação de exceção no Reporting Services](introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services](soapexception-class/reporting-services-soapexception-class.md)  
  
  
