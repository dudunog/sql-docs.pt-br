---
title: Implementando uma classe Command para uma extensão de processamento de dados | Microsoft Docs
description: Saiba como implementar uma classe Command para uma extensão de processamento de dados para que a extensão possa formular solicitações e passá-las para a fonte de dados.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7150b14354be738baa8a127cfe7025dc3245b03e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529515"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>Implementando uma classe Command para uma extensão de processamento de dados
  O objeto **Command** formula uma solicitação e a passa para a fonte de dados. O texto do comando pode ter várias formas sintáticas diferentes, incluindo texto e XML. Se forem retornados resultados, o objeto **Command** retornará resultados como um objeto **DataReader**.  
  
 Para criar uma classe **Command**, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>. Implemente o método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> para retornar um conjunto de resultados como um objeto **DataReader**. O método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> da classe **Command** deve incluir uma implementação que usa uma enumeração <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> como argumento. Se você implantar a sua extensão de processamento de dados no Designer de Relatórios, crie uma implementação que manipule um caso <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> no método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>. Uma implementação somente esquema é usada para fornecer uma lista de campos ao Designer de Relatórios. O objeto **DataReader** retornado pelo método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> precisa conter informações de tipo e de nome para os campos ou colunas, do conjunto de resultados.  
  
 Opcionalmente, a classe **Command** pode implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>. Essa interface permite que uma classe de implementação analise uma consulta e retorne uma lista de parâmetros na consulta. A funcionalidade da interface <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> só será usada no Designer de Relatórios. Quando você implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>, permite que sejam solicitados parâmetros dos usuários do Designer de Relatórios sempre que um relatório for executado em modo de visualização. Além disso, você pode exibir os parâmetros na guia **Parâmetros** da caixa de diálogo **Conjunto de Dados**.  
  
> [!NOTE]  
>  Você não deve implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> se a sua extensão de processamento de dados personalizada não der suporte a parâmetros.  
  
 Para obter uma implementação de exemplo da classe **Command**, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
