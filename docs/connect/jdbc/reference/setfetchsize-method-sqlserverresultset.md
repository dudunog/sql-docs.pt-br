---
description: Método setFetchSize (SQLServerResultSet)
title: Método setFetchSize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d984004b4d306462e2c1345344ebc8072f775a82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431858"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>Método setFetchSize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dá ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias para o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *rows*  
  
 Um **int** que indica o número de linhas a serem buscadas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setFetchSize é especificado pelo método setFetchSize na interface java.sql.ResultSet.  
  
 Se o tamanho de busca especificado for zero, o driver JDBC ignorará o valor e estimará qual deve ser o tamanho da busca. O valor padrão é definido pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que criou o conjunto de resultados. O tamanho de busca pode ser alterado a qualquer momento.  
  
 Esse método altera o tamanho de busca de bloqueio para os cursores do servidor e entra em vigor na próxima vez em que o driver JDBC precisar chamar sp_cursorfetch. Ao definir o tamanho de busca para zero, o tamanho de busca padrão para o tipo de cursor atualmente em uso será restaurado  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
