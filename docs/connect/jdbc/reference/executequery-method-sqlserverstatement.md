---
description: Método executeQuery (SQLServerStatement)
title: Método executeQuery (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeQuery
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 599cf463-e19f-4baa-bacb-513cad7c6cd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f47ae8e9bdf2759adddd3b76d69ae2591da58c19
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437658"
---
# <a name="executequery-method-sqlserverstatement"></a>Método executeQuery (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e retorna um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeQuery é especificado pelo método executeQuery na interface java.sql.Statement.  
  
 [O SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerado se a instrução SQL fornecida produz algo diferente de um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) .  
  
 Se a execução de um procedimento armazenado resultar em uma contagem de atualização maior que um, ou que gere mais de um conjunto de resultados, use o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
