---
description: Transformação Difusão Seletiva
title: Transformação Multicast | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
- sql13.dts.designer.multicasttransformation.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92dd1a4351c9cfdc1bedb0958e370e382b08ecc0
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92197058"
---
# <a name="multicast-transformation"></a>Transformação Difusão Seletiva

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  A transformação Multicast distribui sua entrada em uma ou mais saídas. Essa transformação é semelhante à transformação de divisão condicional. Ambas as transformações dirigem uma entrada para saídas múltiplas. A diferença entre as duas é que a transformação de difusão seletiva dirige todas as linhas para todas as saídas e a divisão condicional dirige uma linha para uma única saída. Para obter mais informações, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
 Configura-se a transformação de difusão seletiva adicionando saídas.  
  
 Usando a transformação de difusão seletiva, um pacote pode criar cópias lógicas de dados. Essa capacidade é útil quando o pacote precisar aplicar vários conjuntos de transformações aos mesmos dados. Por exemplo, uma cópia dos dados é agregada e somente o resumo informativo é carregado em seu destino, enquanto outra cópia dos dados é estendida com valores de pesquisa e colunas derivadas antes que seja carregada em seu destino.  
  
 Essa transformação tem uma entrada e múltiplas saídas. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Configuração da transformação Multicast  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre as propriedades que podem ser definidas programaticamente, consulte [Common Properties](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades deste componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="multicast-transformation-editor"></a>Editor de Transformação Difusão Seletiva
  Use a caixa de diálogo **Editor de Transformação Difusão Seletiva** para exibir e definir as propriedades de cada saída de transformação.  
  
### <a name="options"></a>Opções  
 **Saídas**  
 Selecione uma saída no painel esquerdo para exibir suas propriedades na tabela à direita.  
  
 **Propriedades**  
 Todas as propriedades de saída listadas são somente leitura, exceto **Nome** e **Descrição**.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
