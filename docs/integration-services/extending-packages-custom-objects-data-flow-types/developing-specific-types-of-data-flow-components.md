---
description: Desenvolvendo tipos específicos de componentes de fluxo de dados
title: Desenvolver tipos específicos de componentes de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28f31c63139ddd5ce6b09933411cb600e246de53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484279"
---
# <a name="developing-specific-types-of-data-flow-components"></a>Desenvolvendo tipos específicos de componentes de fluxo de dados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Esta seção aborda as especificações do desenvolvimento de componentes de origem, componentes de transformação com saídas síncronas, componentes de transformação com saídas assíncronas e componentes de destino.  
  
 Para obter informações sobre desenvolvimento de componentes em geral, consulte [Desenvolver um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Desenvolvendo um componente de origem personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contém informações sobre o desenvolvimento de um componente que acessa dados de uma fonte de dados externa e fornece-os a componentes downstream no fluxo de dados.  
  
 [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contém informações sobre o desenvolvimento de um componente de transformação cujas saídas são síncronas para suas entradas. Esses componentes não adicionam dados ao fluxo de dados, mas processam dados percorridos.  
  
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contém informações sobre o desenvolvimento de um componente de transformação cujas saídas não são síncronas para suas entradas. Esses componentes recebem dados de componentes upstream, mas também adicionam dados ao fluxo de dados.  
  
 [Desenvolvendo um componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contém informações sobre o desenvolvimento de um componente que recebe linhas de componentes upstream no fluxo de dados e grava-as em uma fonte de dados externa.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contém as classes e interfaces usadas para criar componentes de fluxo de dados personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contém as classes não gerenciadas e as interfaces da tarefa de fluxo de dados. O desenvolvedor usa esses elementos e o namespace <xref:Microsoft.SqlServer.Dts.Pipeline> gerenciado quando cria um fluxo de dados programaticamente ou cria componentes de fluxo de dados personalizados.  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar soluções de script e objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desenvolver tipos específicos de componentes de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
