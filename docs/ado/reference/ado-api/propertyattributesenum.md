---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 624fa1976792a700342a114f82aa5ca6b75c70ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931568"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica os atributos de um objeto de [Propriedade](../../../ado/reference/ado-api/property-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica que a propriedade não é suportada pelo provedor.|  
|**adPropRequired**|1|Indica que o usuário deve especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropOptional**|2|Indica que o usuário não precisa especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropRead**|512|Indica que o usuário pode ler a propriedade.|  
|**adPropWrite**|1024|Indica que o usuário pode definir a propriedade.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
