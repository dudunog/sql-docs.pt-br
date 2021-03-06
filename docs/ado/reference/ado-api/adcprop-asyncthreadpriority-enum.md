---
description: ADCPROP_ASYNCTHREADPRIORITY_ENUM
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: rothja
ms.author: jroth
ms.openlocfilehash: e01a004ded0b6ed3151ba28c747d3ea245462f92
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976867"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para um objeto de [conjunto de registros](./recordset-object-ado.md) do RDS, especifica a prioridade de execução do thread assíncrono que recupera dados.  
  
 Use essas constantes com a propriedade dinâmica "**prioridade de thread em segundo plano**" do **conjunto de registros** , que é referenciada no índice de propriedade dinâmica do ADO para OLE DB e documentada no [serviço de cursor da Microsoft para OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Define a prioridade entre normal e mais alta.|  
|**adPriorityBelowNormal**|2|Define a prioridade entre a mais baixa e a normal.|  
|**adPriorityHighest**|5|Define a prioridade para o mais alto possível.|  
|**AdPriorityLowest**|1|Define a prioridade para o mais baixo possível.|  
|**adPriorityNormal**|3|Define a prioridade como normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. mais alto|  
|AdoEnums. AdcPropAsyncThreadPriority. mais baixo|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|