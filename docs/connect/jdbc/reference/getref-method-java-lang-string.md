---
title: Método getRef (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getRef (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a8ff2dd5-923b-4a2f-ab33-665574b2dfda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd5b2019d31e84406d9386d180b87213273d0389
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980572"
---
# <a name="getref-method-javalangstring"></a>Método getRef (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto Ref na linguagem de programação Java, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Ref getRef(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Ref.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getRef é especificado pelo método getRef na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getRef &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
