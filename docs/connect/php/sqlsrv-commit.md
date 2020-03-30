---
title: sqlsrv_commit | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_commit
apitype: NA
helpviewer_keywords:
- transaction support
- API Reference, sqlsrv_commit
- sqlsrv_commit
ms.assetid: bad67571-61ad-45b5-b4ff-677e3544f809
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13c4f2534ec49c1d3467045d778e0c446f972573
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67992855"
---
# <a name="sqlsrv_commit"></a>sqlsrv_commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Confirma a transação atual na conexão especificada e retorna a conexão para o modo de confirmação automática. A transação atual inclui todas as instruções na conexão especificada que foram executadas após a chamada para [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md) e antes de qualquer chamada para [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) ou **sqlsrv_commit**.  
  
> [!NOTE]  
> O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está no modo de confirmação automática por padrão. Isso significa que todas as consultas são confirmadas automaticamente quando obtêm êxito, exceto se foram designadas como parte de uma transação explícita usando **sqlsrv_begin_transaction**.  
  
> [!NOTE]  
> Se **sqlsrv_commit** for chamado em uma conexão que não está em uma transação ativa e que foi iniciada com **sqlsrv_begin_transaction**, a chamada retornará **false** e um erro *Fora de Transação* será adicionado à coleção de erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_commit( resource $conn )  
```  
  
#### <a name="parameters"></a>parâmetros  
*$conn*: a conexão em que a transação está ativa.  
  
## <a name="return-value"></a>Valor retornado  
Um valor booliano: **true** se a transação foi confirmada com êxito. Caso contrário, **false**.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir executa duas consultas como parte de uma transação. Se ambas as consultas forem bem-sucedidas, a transação será confirmada. Se uma das consultas falhar (ou ambas), a transação será revertida.  
  
A primeira consulta no exemplo insere uma nova ordem de venda na tabela *Sales.SalesOrderDetail* do banco de dados AdventureWorks. A ordem é de cinco unidades do produto com a identificação 709. A segunda consulta reduz a quantidade de estoque do produto com a identificação do produto 709 em cinco unidades. Essas consultas estão incluídas em uma transação porque ambas devem ter êxito para que o banco de dados reflita com precisão o estado dos pedidos e a disponibilidade do produto.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if (sqlsrv_begin_transaction( $conn) === false)  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and execute the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Com a finalidade de nos concentrarmos no comportamento transacional, alguns tratamentos de erro recomendados não estão incluídos no exemplo anterior. Para um aplicativo de produção, recomenda-se que todas as chamadas para a função **sqlsrv** contenham verificação e tratamento de erros.  
  
> [!NOTE]  
> Não use o Transact-SQL inserido para executar transações. Por exemplo, não execute uma instrução com "BEGIN TRANSACTION" como a consulta Transact-SQL para iniciar uma transação. O comportamento transacional esperado não pode ser garantido ao usar o Transact-SQL inserido para executar transações.  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Como executar transações](../../connect/php/how-to-perform-transactions.md)

[Visão geral dos Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
  
