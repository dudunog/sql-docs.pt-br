---
title: Configurações de informações de dispositivo XML | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee4e9f30dc190aae78e1e3e763451e42b3a52ecb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65571019"
---
# <a name="xml-device-information-settings"></a>Configurações de informações do dispositivo XML
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato XML.  
  
|Configuração|Valores|Detalhes|  
|-------------|------------|-------------|  
|**XSLT**|O caminho no namespace do servidor de relatório de um XSLT a ser aplicado ao arquivo XML. Por exemplo, **/Transforms/myxslt**.|O arquivo xsl deve ser um recurso publicado no servidor de relatório e você deve acessá-lo por meio de um caminho de item do servidor de relatório. O valor dessa configuração é aplicado depois de qualquer XSLT especificado no relatório. Se a configuração **XSLT** for aplicada, a configuração **OmitSchema** será ignorada.|  
|**MIMEType**|O tipo MIME (Multipurpose Internet Mail Extensions) do arquivo XML.||  
|**UseFormattedValues**|**true**<br /><br /> **false**|Indica se será preciso renderizar o valor formatado de uma caixa de texto durante a geração dos dados XML.<br /><br /> Um valor falso indica que o valor subjacente da caixa de texto será usado.|  
|**Indented**|**true**<br /><br /> **false**|Indica se será preciso gerar XML recuado. O valor padrão **false** gera XML não recuado e compactado.|  
|**OmitNamespace**|**true**<br /><br /> **false**|Indica se será preciso omitir o namespace padrão do XML.<br /><br /> Se true, o XML não especifica um namespace padrão.<br /><br /> Se false, o XML especifica um namespace padrão com o valor da propriedade DataSchema do relatório. A propriedade DataSchema usa como padrão o nome do relatório.<br /><br /> O valor padrão é**false**.|  
|**OmitSchema**|**true**<br /><br /> **false**|Indica se será preciso omitir o local de esquema do XML. O local é o atributo SchemaLocation.<br /><br /> O valor padrão de OmitSchema depende do valor de OmitNamespace:<br /><br /> Se OmitNamespace = False, OmitSchema = **False** por padrão. O usuário pode substituir o padrão definindo OmitSchema = True.<br /><br /> Se OmitNamespace = True, OmitSchema funcionará como **True** , independentemente do valor configurado explicitamente para OmitShema.|  
|**Codificação**|O nome da IANA (Internet Assigned Numbers Authority) de uma codificação de caracteres com suporte do .NET Framework.|O valor padrão é **UTF-8**. Exemplos de outros valores incluem ASCII, UTF-7 e UTF-16.|  
|**FileExtension**|A extensão de arquivo a ser usada para o arquivo gerado.||  
|**Esquema**|Um valor **true** indica que um esquema XML será renderizado. O valor padrão é **false**.|Indica se será preciso renderizar o XSD (XML schema definition) ou se os dados XML reais serão renderizados.|  
  
## <a name="see-also"></a>Consulte Também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
