---
title: Método getBytes (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe3dc103480899ccf5d174ca2a802cdee1c9a314
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921639"
---
# <a name="getbytes-method-javalangstring"></a>Método getBytes (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como uma matriz de valores bytes, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Uma matriz de valores **byte**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Em uma versão anterior do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], era possível usar o SQLServerCallableStatement.getBytes para converter valores entre matrizes de bytes e o tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**date**, **time**, **datetime2** ou **datetimeoffset**. Agora, ao usar esse método com esses tipos de dados, ocorrerá uma exceção indicando que não há suporte para a conversão.  
  
 Esse método getBytes é especificado pelo método getBytes na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBytes &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
