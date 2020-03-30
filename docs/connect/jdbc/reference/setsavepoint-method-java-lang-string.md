---
title: Método setSavepoint (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cae36f62cba9f7c8b97ae13c06d1f01960f616e8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973093"
---
# <a name="setsavepoint-method-javalangstring"></a>Método setSavepoint (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um ponto de salvamento com o nome fornecido na transação atual e retorna o novo objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) que o representa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sName*  
  
 Um valor **cadeia de caracteres** que contém o nome do ponto de salvamento.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto SavePoint.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setSavePoint é especificado pelo método setSavePoint na interface java.sql.Connection.  
  
 O argumento *sName* é escapado automaticamente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Método setSavepoint &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
