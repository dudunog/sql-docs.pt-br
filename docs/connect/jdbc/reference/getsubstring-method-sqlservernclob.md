---
description: Método getSubString (SQLServerNClob)
title: Método getSubString (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fb3e1d0df17c71f915d34c202fcf1c4b4960a6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434298"
---
# <a name="getsubstring-method-sqlservernclob"></a>Método getSubString (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma cópia da subcadeia de caracteres especificada no **NCLOB** com base na posição inicial especificada e no número de caracteres a serem copiados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSubString(long pos,  
                                  int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 O primeiro caractere da subcadeia a ser extraído. O primeiro caractere está na posição 1.  
  
 *length*  
  
 O número de caracteres consecutivos a serem copiados.  
  
## <a name="return-value"></a>Valor de retorno  
 Uma **cadeia de caracteres** que é a subcadeia especificada no **NCLOB**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSubString é especificado pelo método getSubString na interface java.sql.NClob.  
  
 A tentativa de obter zero caracteres de um NCLOB nulo ou de comprimento zero retorna uma cadeia de caracteres vazia. Tentar obter qualquer comprimento de caracteres em qualquer posição que não seja a posição 1 em um NCLOB de comprimento zero fará com que uma exceção de posição seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
