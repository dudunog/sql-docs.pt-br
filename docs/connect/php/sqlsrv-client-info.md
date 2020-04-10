---
title: sqlsrv_client_info | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d17d3a49a241ee1ff042fceb3602b1d84f2cca9b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920115"
---
# <a name="sqlsrv_client_info"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna informações sobre a conexão e a pilha do cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>parâmetros  
*$conn*: o recurso de conexão pelo qual o cliente está conectado.  
  
## <a name="return-value"></a>Valor retornado  
Uma matriz associativa com chaves descritas na tabela abaixo, ou **false** , se o recurso de conexão for nulo.  
  
**Para versões 3.2 e 3.1 do PHP para SQL Server**:  
  
|Chave|DESCRIÇÃO|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (ODBC Driver 11 for SQL Server)|  
|DriverODBCVer|Versão do ODBC (xx.yy)|  
|DriverVer|Versão do ODBC Driver 11 for SQL Server:<br /><br />xx.yy.zzzz ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.2 ou 3.1)|  
|ExtensionVer|versão do php_sqlsrv.dll:<br /><br />3.2.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.2)<br /><br />3.1.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.1)|  
  
**Para versões 3.0 e 2.0 do PHP para SQL Server**:  
  
|Chave|DESCRIÇÃO|  
|-------|---------------|  
|DriverDllName|SQLNCLI10.DLL ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
|DriverODBCVer|Versão do ODBC (xx.yy)|  
|DriverVer|Versão de DLL do SQL Server Native Client:<br /><br />10.50.xxx ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
|ExtensionVer|versão do php_sqlsrv.dll:<br /><br />2.0.xxxx.x ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir grava informações do cliente no console quando o exemplo é executado na linha de comando. O exemplo supõe que o SQL Server esteja instalado no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
