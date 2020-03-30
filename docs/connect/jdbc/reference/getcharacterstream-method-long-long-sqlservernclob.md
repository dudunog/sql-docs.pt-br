---
title: Método getCharacterStream (long, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 10cd57cff29c73a2b99d1489eb122eed37859768
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953279"
---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>Método getCharacterStream (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os dados de **NCLOB** como um objeto **Reader** ou como um fluxo de caracteres com uma posição e um comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                  long length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 Um **long** que indica o deslocamento do primeiro caractere do valor parcial a ser recuperado.  
  
 *length*  
  
 Um **long** que indica o comprimento, em caracteres, do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Reader que contém os dados **NCLOB**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface java.sql.NClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getCharacterStream &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
