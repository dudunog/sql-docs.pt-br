---
description: Evento onReadyStateChange (RDS)
title: Evento onReadyStateChange (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: rothja
ms.author: jroth
ms.openlocfilehash: ee9f48a3cba1190cdd9400b5ee5ecb30c35bfaed
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724447"
---
# <a name="onreadystatechange-event-rds"></a>Evento onReadyStateChange (RDS)
O evento **onReadyStateChange** é chamado sempre que o valor da propriedade [ReadyState](./readystate-property-rds.md) é alterado.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ReadyState** reflete o progresso de um [RDS. O objeto DataControl](./datacontrol-object-rds.md) como ele recupera dados de forma assíncrona em seu objeto [Recordset](../ado-api/recordset-object-ado.md) . Use o evento **onReadyStateChange** para monitorar as alterações na propriedade **ReadyState** sempre que elas ocorrerem. Isso é mais eficiente do que verificar periodicamente o valor da propriedade.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../guide/data/ado-event-handler-summary.md)