---
description: Método getNString (java.lang.String) (SQLServerResultSet)
title: Método getNString (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 103ee0edb740c4ca23ee36e60e41ee8e54ef0cec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435218"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>Método getNString (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto java.lang.String.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Uma Cadeia de Caracteres que contém o rótulo da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto String.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getNString é especificado pelo método getNString na interface do java.sql.SQLServerResultSet.  
  
 Esse método pode ser usado para recuperar o valor de uma coluna **nvarchar**, **nchar**, **nvarchar (max)**, **ntext** ou **xml** na linha atual deste objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Se você tentar usar esse método para recuperar valores de outros tipos de dados, uma exceção será lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getNString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
