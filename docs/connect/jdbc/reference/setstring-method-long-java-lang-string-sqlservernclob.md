---
title: Método setString (long, java.lang.String) - NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c549d3e1b7b9b63663333a59b263a2aa6ad4113
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972670"
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>Método setString (long, java.lang.String) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava a **String** especificada em **NCLOB**, começando na posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no **NCLOB**; a primeira posição é 1.  
  
 *str*  
  
 A String a ser gravada no **NCLOB**.  
  
## <a name="return-value"></a>Valor retornado  
 O número de caracteres gravados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setString é especificado pelo método setString na interface java.sql.NClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
