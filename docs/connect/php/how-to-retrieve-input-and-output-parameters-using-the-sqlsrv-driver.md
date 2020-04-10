---
title: Como recuperar parâmetros de E/S usando o SQLSRV Driver | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 9a7c5f60-67f9-4968-a3a8-c256ee481da2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2bad5942e98271638b4b929d55c54c1562629e44
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916072"
---
# <a name="how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver"></a>Como recuperar parâmetros de entrada e de saída usando o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico demonstra como usar o driver SQLSRV para chamar um procedimento armazenado no qual um parâmetro foi definido como parâmetro de entrada/saída e como recuperar os resultados. Ao recuperar um parâmetro de saída ou de entrada/saída, todos os resultados retornados pelo procedimento armazenado devem ser consumidos antes que o valor do parâmetro retornado esteja acessível.  
  
> [!NOTE]  
> Variáveis que são inicializadas ou atualizadas para **null**, **DateTime**ou tipos de fluxo não podem ser usadas como parâmetros de saída.  
  
## <a name="example-1"></a>Exemplo 1
O exemplo a seguir chama um procedimento armazenado que subtrai horas de férias usadas das horas de férias disponíveis de um funcionário especificado. A variável que representa as horas de férias usadas, *$vacationHrs*, é passada para o procedimento armazenado como um parâmetro de entrada. Depois de atualizar as horas de férias disponíveis, o procedimento armazenado usa o mesmo parâmetro para retornar o número de horas de férias restantes.  
  
> [!NOTE]  
> Inicializar *$vacationHrs* como 4 define o PHPTYPE retornado como inteiro. Para garantir a integridade do tipo de dados, os parâmetros de entrada/saída devem ser inicializados antes de chamar o procedimento armazenado ou o PHPTYPE desejado deve ser especificado. Para obter informações sobre como especificar o PHPTYPE, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Como o procedimento armazenado retorna dois resultados, [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md) deve ser chamado depois que o procedimento armazenado for executado para disponibilizar o valor do parâmetro de saída. Depois de chamar **sqlsrv_next_result**, *$vacationHrs* conterá o valor do parâmetro de saída retornado pelo procedimento armazenado.  
  
> [!NOTE]  
> Chamar os procedimentos armazenados usando a sintaxe canônica é a prática recomendada. Para obter mais informações sobre a sintaxe canônica, veja [Como chamar um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
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
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = "CREATE PROCEDURE SubtractVacationHours  
                        @EmployeeID int,  
                        @VacationHrs smallint OUTPUT  
                  AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHrs  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHrs = (SELECT VacationHours  
                                      FROM HumanResources.Employee  
                                      WHERE EmployeeID = @EmployeeID)";  
  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call SubtractVacationHours( ?, ?)}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an INOUT  
parameter. Initializing $vacationHrs to 8 sets the returned PHPTYPE to  
integer. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
  
$employeeId = 4;  
$vacationHrs = 8;  
$params = array(   
                 array($employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $vacationHrs. */  
sqlsrv_next_result($stmt3);  
echo "Remaining vacation hours: ".$vacationHrs;  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> Ao associar um parâmetro de entrada/saída a um tipo bigint, se o valor puder terminar fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), será necessário especificar seu tipo de campo SQL como SQLSRV_SQLTYPE_BIGINT. Caso contrário, isso poderá resultar em uma exceção de "valor fora do intervalo".

## <a name="example-2"></a>Exemplo 2
Este exemplo de código mostra como associar um valor bigint grande como um parâmetro de entrada/saída.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_INOUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>Consulte Também  
[Como especificar a direção do parâmetro usando o driver SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[Como recuperar parâmetros de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[Recuperando dados](../../connect/php/retrieving-data.md)  
  
