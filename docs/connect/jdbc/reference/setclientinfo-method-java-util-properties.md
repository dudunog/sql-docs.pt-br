---
title: Método setClientInfo (java.util.Properties) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d89d266af2ef2409fb0a1a06c4768a0f2c387ce7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920912"
---
# <a name="setclientinfo-method-javautilproperties"></a>Método setClientInfo (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor das propriedades de informações de cliente da conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *properties*  
  
 Um objeto Properties que contém a lista das propriedades information do cliente para definir.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setClientInfo é especificado pelo método setClientInfo na interface java.sql.Connection.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não é compatível com nenhuma propriedade de informações do cliente. Esse método vai gerar avisos se o parâmetro de entrada *properties* não se referir a um conjunto vazio de propriedades. Em outras palavras, este método gerará avisos para as propriedades que o aplicativo quiser definir. Os aplicativos devem usar o método [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) da classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) para recuperar cada aviso.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
