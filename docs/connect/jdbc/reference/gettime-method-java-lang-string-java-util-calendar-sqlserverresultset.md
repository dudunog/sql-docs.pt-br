---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 13b51f77-cec9-45fc-862e-3d2bb2d718d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b66a142789e855eaf0e4524554892ea85c7b9cbe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979069"
---
# <a name="gettime-method-javalangstring-javautilcalendar-sqlserverresultset"></a>Método getTime (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto java.sql.Time na linguagem de programação Java usando o objeto Calendar fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Time getTime(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *colName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *cal*  
  
 Um objeto Calendar.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Time.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTime é especificado pelo método getTime na interface java.sql.ResultSet.  
  
 Esse método retorna uma parte de hora válida de um tipo de dados datetime ou smalldatetime do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], com a parte de data definida como a data de linha de base do Java de 1970/01/01 no fuso horário do Calendário fornecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
