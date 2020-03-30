---
title: PDO::errorInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe0f0cc2ec15fcdb871f290f03565482a8477995
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67936265"
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera informações de erro estendidas da operação mais recente no identificador do banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>Valor retornado  
Uma matriz de informações de erro sobre a operação mais recente no identificador do banco de dados. A matriz consiste nos seguintes campos:  
  
-   O código de erro SQLSTATE.  
  
-   O código de erro específico do driver.  
  
-   A mensagem de erro específica do driver.  
  
Se não houver nenhum erro ou se o SQLSTATE não estiver definido, os campos específicos do driver serão NULL.  
  
## <a name="remarks"></a>Comentários  
PDO::errorInfo recupera somente informações de erro de operações realizadas diretamente no banco de dados. Use PDOStatement::errorInfo quando uma instância de PDOStatement for criada usando PDO::prepare ou PDO::query.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Neste exemplo, o nome da coluna está incorreto, `Cityx` em vez de `City`, causando um erro, que é, então, relatado.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
