---
title: Usando a classe RenderedOutputFile para uma extensão de entrega | Microsoft Docs
description: Saiba como as extensões de entrega podem usar a classe RenderedOutputFile, que armazena um relatório renderizado ou recursos de relatório.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f743227a2927ad97c5a0bcc76c3634726969caef
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529102"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Usando a classe RenderedOutputFile para uma extensão de entrega
  A classe de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> representa um fluxo de dados e informações sobre as propriedades associadas ao fluxo de dados. A propriedade **Data** da classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> é usada para representar um relatório renderizado ou relatar um recurso como um objeto **Stream**.  
  
 O método <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> do objeto **Report** retorna uma matriz de um ou mais objetos <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> que juntos constituem um único relatório renderizado. O primeiro objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> é o relatório renderizado. Qualquer outro objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> será o recurso a ser entregue junto com os dados de relatório (por exemplo, um arquivo HTML e as imagens associadas). A renderização de extensões que são extensões de renderização de fluxo único (IMAGE, PDF, MHTML e EXCEL) retornará só um objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> na matriz.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
