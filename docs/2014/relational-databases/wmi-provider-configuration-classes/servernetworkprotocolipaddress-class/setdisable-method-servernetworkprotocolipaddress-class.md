---
title: Método SetDisable (classe ServerNetworkProtocolIPAddress) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: adaa66fd04f6e3b6f97b4e4edc75d9a21ea4e31f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62643221"
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>Método SetDisable (classe ServerNetworkProtocolIPAddress)
  Desabilita o endereço IP.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto [ServerNetworkProtocolIPAdress Class] ServerNetworkProtocolIPAddress-class.md) que representa um endereço IP para o protocolo de rede em uma instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]do.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
