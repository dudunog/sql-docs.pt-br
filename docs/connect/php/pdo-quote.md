---
title: PDO::quote
description: Referência da API para a função PDO::quote no Driver PDO_SQLSRV da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31756cbc2f0ede497ea34077f1bdd760412c716c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081835"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Processa uma cadeia de caracteres para uso em uma consulta, colocando a cadeia de caracteres de entrada entre aspas, conforme exigido pelo banco de dados do SQL Server subjacente. O PDO::quote insere um caractere de escape antes de caracteres especiais na cadeia de caracteres de entrada, usando um estilo de aspas adequado ao SQL Server.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*string*: a cadeia de caracteres a ser cotada.  
  
$*parameter_type*: um símbolo opcional (inteiro) que indica o tipo de dados.  O padrão é PDO::PARAM_STR.  

Novas constantes PDO foram introduzidas no PHP 7.2 para adicionar suporte para [cadeias de caracteres Unicode e não Unicode de associação](https://wiki.php.net/rfc/extended-string-types-for-pdo). As cadeias de caracteres Unicode podem ser colocadas entre aspas com um N como prefixo (ou seja, N"cadeia de caracteres" em vez de "cadeia de caracteres").

1. PDO::P ARAM_STR_NATL – um novo tipo de cadeias de caracteres Unicode, a ser aplicado como um bitwise-OR para PDO::PARAM_STR
1. PDO::P ARAM_STR_CHAR – um novo tipo de cadeias de caracteres não Unicode, a ser aplicado como um bitwise-OR para PDO::PARAM_STR
1. PDO:: ATTR_DEFAULT_STR_PARAM – configure como PDO::PARAM_STR_NATL ou PDO::PARAM_STR_CHAR para indicar um valor para bitwise-OR para PDO::PARAM_STR por padrão

Com a versão 5.8.0 será possível usar essas constantes com PDO::quote.
  
## <a name="return-value"></a>Valor de retorno  
Uma cadeia de caracteres entre aspas que pode ser passada para uma instrução SQL, ou false em caso de falha.  
  
## <a name="remarks"></a>Comentários  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="string-escape-example"></a>Exemplo de escape de cadeia de caracteres  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="pdo-quote-example"></a>Exemplo de cotação de PDO  

O script a seguir mostra alguns exemplos de como os tipos de cadeia de caracteres estendidos afetam PDO::quote() com o PHP 7.2+.

```
<?php
$database = "test";
$server = "(local)";
$db = new PDO("sqlsrv:server=$server; Database=$database", "", "");

$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL); // N'über'
$db->quote('foo'); // 'foo'

$db->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$db->quote('über'); // N'über'
$db->quote('foo', PDO::PARAM_STR | PDO::PARAM_STR_CHAR); // 'foo'
?>
```
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
