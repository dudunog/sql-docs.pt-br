---
title: Método SetCurrentCertificate (classe SecurityCertificate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetCurrentCertificate Method (SecurityCertificate Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 32af70857eac43a99257444081c1bcbdc842a2e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63270637"
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>Método SetCurrentCertificate (classe SecurityCertificate)
  Define o certificado de segurança atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetCurrentCertificate(  
SHA , SQLInstance  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto [SecurityCertificate Class] SecurityCertificate-class.md) que representa um certificado de segurança.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*SHA*|Um valor da cadeia de caracteres que especifica a impressão digital de SHA (algoritmo de hash seguro) para o certificado de segurança necessário.|  
|*SQLInstance*|Um valor da cadeia de caracteres que especifica a instância para a qual o certificado é necessário.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
