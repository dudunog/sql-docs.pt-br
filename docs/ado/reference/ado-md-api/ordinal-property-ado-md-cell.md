---
description: Propriedade Ordinal (Célula do ADO MD)
title: Propriedade ordinal (célula ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: rothja
ms.author: jroth
ms.openlocfilehash: b4d14b2cdfc61fd76221a2071f15593807b5f1ba
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986217"
---
# <a name="ordinal-property-ado-md-cell"></a>Propriedade Ordinal (Célula do ADO MD)
Identifica exclusivamente uma [célula](./cell-object-ado-md.md) pela sua posição em um células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 O valor ordinal da célula identifica exclusivamente a célula em um células. Conceitualmente, as células são numeradas em um células como se o células fosse uma matriz *p*-dimensional, em que *p* é o número de [eixos](./axes-collection-ado-md.md). As células são numeradas a partir de zero na ordem de linha principal. Aqui está a fórmula para calcular o número ordinal de uma célula:  
  
 O valor ordinal da célula pode ser usado com a propriedade [Item](./item-property-ado-md-cellset.md) do objeto [células](./cellset-object-ado-md.md) para recuperar rapidamente a [célula](./cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de eixo (VBScript)](./axis-example-vbscript.md)   
 [Objeto células (ADO MD)](./cellset-object-ado-md.md)   
 [Propriedade Item (ADO MD células)](./item-property-ado-md-cellset.md)   
 [Propriedade Ordinal (Posição do ADO MD)](./ordinal-property-ado-md-position.md)