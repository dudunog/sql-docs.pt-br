---
title: Como tratar erros e avisos usando o driver SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0605fc5a0fc27abfbcd15c22d5553587eecb0349
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916249"
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>Como tratar erros e avisos usando odriver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Por padrão, o driver SQLSRV trata avisos como erros; uma chamada para uma função **sqlsrv** que gere um erro ou um aviso retornará **false**. Este tópico demonstra como desativar esse comportamento padrão e como tratar avisos e erros separadamente.  
  
> [!NOTE]  
> Há algumas exceções para o comportamento padrão de tratamento de avisos como erros. Os avisos que correspondem aos valores SQLSTATE 01000, 01001, 01003 e 01S02 nunca são tratados como erros.  
  
## <a name="example"></a>Exemplo  
O exemplo de código a seguir usa duas funções definidas pelo usuário, **DisplayErrors** e **DisplayWarnings**, para tratar erros e avisos. O exemplo demonstra como tratar avisos e erros separadamente da seguinte forma:  
  
1.  Desativa o comportamento padrão de tratamento de avisos como erros.  
  
2.  Cria um procedimento armazenado que atualiza as horas de férias de um funcionário e retorna as horas de férias restantes como um parâmetro de saída. Quando as horas de férias disponíveis de um funcionário forem negativas, o procedimento armazenado imprimirá um aviso.  
  
3.  Atualiza as horas de férias de vários funcionários chamando o procedimento armazenado para cada funcionário e exibe as mensagens que correspondem aos avisos e erros que ocorrem.  
  
4.  Exibe as horas de férias restantes para cada funcionário.  
  
Na primeira chamada para uma função **sqlsrv** ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)), os avisos são tratados como erros. Como os avisos são adicionados à coleção de erros, não é necessário verificar se há avisos separadamente dos erros. Porém, nas chamadas subsequentes para as funções **sqlsrv** , os avisos não serão tratados como erros, por isso, é necessário verificar explicitamente os avisos e erros.  
  
Observe também que o código de exemplo verifica erros após cada chamada para uma função **sqlsrv** . Essa é a prática recomendada.  
  
Este exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando. Quando o exemplo for executado em uma nova instalação do banco de dados AdventureWorks, ele produzirá três avisos e dois erros. Os dois primeiros são avisos padrão, emitidos quando você se conecta a um banco de dados. O terceiro aviso ocorre porque as horas de férias disponíveis de um funcionário são atualizadas para um valor negativo. O erro ocorre porque as horas de férias disponíveis de um funcionário são atualizadas para um valor menor que -40 horas, que é uma violação de uma restrição na tabela.  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to subtract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Como configurar o tratamento de erro e de avisos usando o driver SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
