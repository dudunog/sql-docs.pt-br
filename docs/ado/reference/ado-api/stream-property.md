---
description: Propriedade Stream
title: Propriedade de fluxo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b00d145dfd718c64bbd3a87d6df353114afcb2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441838"
---
# <a name="stream-property"></a>Propriedade Stream
Obtém ou define um objeto de **fluxo** de OLE DB de/em um objeto **ADOStreamConstruction** .  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppStream*  
 Ponteiro para um objeto de **fluxo** de OLE DB.  
  
 *pStream*  
 Um objeto de **fluxo** OLE DB.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão. Isso inclui S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [ADOStreamConstruction Interface](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
