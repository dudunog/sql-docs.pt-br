---
description: Método getConnection (java.lang.String, java.lang.String)
title: Método getConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bfc2a318fad442edcae2af4df1a51c521ed9bda9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436538"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>Método getConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão com a fonte de dados que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) representa usando o nome de usuário e a senha fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *username*  
  
 Uma **String** que contém o nome do usuário.  
  
 *password*  
  
 Uma **String** que contém a senha.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método getConnection é especificado pelo método getConnection na interface javax.sql.DataSource.  
  
 Chamar o método getConnection com um nome de usuário ou uma senha não nulos substituirá as propriedades do nome de usuário e da senha que são definidas na classe SQLServerDataSource ao inicializar o objeto SQLServerConnection. Por exemplo, se o chamador chamou [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) e [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) na fonte de dados e, em seguida, chamar getConnection e fornecer um nome de usuário não nulo ou uma senha não nula, o nome de usuário e a senha definidos por setUser e setPassword serão substituídos pelo nome de usuário e pela senha transmitidos ao getConnection.  
  
> [!NOTE]  
>  O nome de usuário e a senha que são definidos dentro da URL usando uma chamada ao método [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) não serão alterados nesse caso.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
