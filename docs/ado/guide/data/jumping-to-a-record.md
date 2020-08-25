---
description: Saltar para um registro
title: Saltando para um registro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: rothja
ms.author: jroth
ms.openlocfilehash: dcbdf68a7d79b64e25dcb700b989628a6a72b8e2
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805860"
---
# <a name="jumping-to-a-record"></a>Saltar para um registro
O método [move](../../reference/ado-api/move-method-ado.md) permite que você avance ou regressiva no **conjunto** de registros um número especificado de registro usando a seguinte sintaxe:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Comentários  
 Há suporte para o método **move** em todos os objetos **Recordset** .  
  
 Se o argumento *NumRecords* for maior que zero, a posição do registro atual avançará (em direção ao final do **conjunto de registros**). Se *NumRecords* for menor que zero, a posição do registro atual mudará para trás (em direção ao início do **conjunto de registros**).  
  
 Se a chamada de **movimentação** mover a posição do registro atual para um ponto antes do primeiro registro, o ADO definirá o registro atual como a posição anterior ao primeiro registro no **conjunto de registros** (**BOF** é **true**). Uma tentativa de retroceder quando a propriedade **BOF** já é **verdadeira** gera um erro.  
  
 Se a chamada de **movimentação** mover a posição do registro atual para um ponto após o último registro, o ADO definirá o registro atual como a posição após o último registro no **conjunto de registros** (**EOF** é **true**). Uma tentativa de avançar quando a propriedade **EOF** já é **verdadeira** gera um erro.  
  
 Chamar o método **move** de um objeto **Recordset** vazio gera um erro.  
  
 Se você passar um indicador no argumento *Start* , a movimentação será relativa ao registro com esse indicador, supondo que o objeto **Recordset** dê suporte a indicadores. Um indicador é obtido usando a propriedade [Bookmark](../../reference/ado-api/bookmark-property-ado.md) . Se não for especificado, a movimentação será relativa ao registro atual.  
  
 Se você estiver usando a propriedade **CacheSize** para armazenar localmente os registros do provedor, passar um argumento *NumRecords* que move a posição do registro atual para fora do grupo atual de registros em cache força o ADO a recuperar um novo grupo de registros, a partir do registro de destino. A propriedade **CacheSize** determina o tamanho do grupo recuperado recentemente e o registro de destino é o primeiro registro recuperado.