---
title: Propriedade SupportAlias (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6fd06ad0921dbb113a89af77e46733a28c2226c9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061410"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Propriedade SupportAlias (classe ClientNetworkProtocol)
  Obtém a propriedade booliana que especifica se o protocolo de rede atual especificado pelo [método Setordenavalue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) dá suporte a aliases.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor Booliano que especifica se o protocolo de rede de cliente dá suporte a aliases.  
  
 Se True, o protocolo de rede de cliente dá suporte a aliases.  
  
 Se False, o protocolo de rede de cliente não dá suporte a aliases.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
