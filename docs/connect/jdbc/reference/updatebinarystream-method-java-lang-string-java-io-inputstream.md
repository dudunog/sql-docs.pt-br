---
description: Método updateBinaryStream (java.lang.String, java.io.InputStream)
title: Método updateBinaryStream (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e642ada792f9355df9cc9be37ce8fbc76c85125
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354102"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>Método updateBinaryStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo binário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que contém o rótulo da coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateBinaryStream é especificado pelo método updateBinaryStream na interface java.sql.ResultSet.  
  
 O uso desse método nos tipos de dados **image**, **text** e **ntext** do SQL Server pode afetar o desempenho.  
  
 Esse método passa bytes de um objeto InputStream para colunas binárias [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selecionadas do como binary, varbinary, varbinary(max), image, xml e udt. Não há suporte para a atualização de colunas de caracteres nesse método. Para atualizar colunas de caracteres com um InputStream, use o método [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
