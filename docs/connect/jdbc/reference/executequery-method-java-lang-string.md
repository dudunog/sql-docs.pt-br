---
title: Método executeQuery (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38e5a31ccaf493a8800f0e15abd1c21424db07c7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954817"
---
# <a name="executequery-method-javalangstring"></a>Método executeQuery (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e retorna um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeQuery é especificado pelo método executeQuery na interface java.sql.Statement.  
  
 Esse método substitui o método [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) que é localizado na classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
 Chamar esse método resultará em uma exceção, uma vez que a instrução SQL para o objeto SQLServerPreparedStatement é especificada quando o objeto é criado.  
  
 [O SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerado se a instrução SQL fornecida produz algo diferente de um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Método executeQuery &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
