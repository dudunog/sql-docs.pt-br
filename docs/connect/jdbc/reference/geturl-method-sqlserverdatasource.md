---
title: Método getURL (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f3922e5cf97b6c7b5a795f295249950fd21a9f3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978202"
---
# <a name="geturl-method-sqlserverdatasource"></a>Método getURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a URL usada para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém a URL.  
  
## <a name="remarks"></a>Comentários  
 Por motivos de segurança, não inclua a senha na URL fornecida ao método [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md). Isso porque os Servidores de Aplicativos Java de terceiros muito frequentemente exibirão o valor definido para a propriedade URL em suas respectivas interfaces de usuário da configuração da fonte de dados. Em vez disso, use o método [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) para definir o valor da senha. Os Servidores de Aplicativos Java não exibirão uma senha que é definida em suas respectivas fontes de dados na interface de usuário da configuração.  
  
> [!NOTE]  
>  Se o método setURL não for chamado antes do método getURL, getURL retornará o valor padrão de “jdbc:sqlserver://”.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
