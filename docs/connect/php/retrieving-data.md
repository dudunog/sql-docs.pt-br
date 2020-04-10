---
title: Recuperação de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 050197fe67724dba3ab2cb3c0de53661487b9ef5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928393"
---
# <a name="retrieving-data"></a>Recuperando dados
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico e os tópicos desta seção discutem como recuperar dados.  
  
## <a name="sqlsrv-driver"></a>Driver SQLSRV  
O driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] fornece as seguintes opções para recuperar dados de um conjunto de resultados:  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> Quando você usar qualquer uma das funções mencionadas acima, evite comparações com null como critério para sair de loops. Como as funções **sqlsrv** retornam false quando ocorre um erro, o código a seguir pode resultar em um loop infinito na ocorrência de um erro em [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md):  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
Se a sua consulta recuperar mais de um conjunto de resultados, você poderá continuar para o próximo conjunto de resultados com [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md).  
  
Da versão 1.1 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] em diante, você pode usar [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) para ver se um conjunto de resultados tem linhas.  
  
## <a name="pdo_sqlsrv-driver"></a>Driver PDO_SQLSRV  
O driver PDO_SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] fornece as seguintes opções para recuperar dados de um conjunto de resultados:  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
Se a sua consulta recuperar mais de um conjunto de resultados, você poderá continuar para o próximo conjunto de resultados com [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md).  
  
Você pode ver quantas linhas estão em um conjunto de resultados se especificar um cursor rolável e, em seguida, chamar [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md).  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) permite que você especifique um tipo de cursor. Depois, com [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) você pode selecionar uma linha. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para obter mais informações e um exemplo.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|---------|---------------|  
|[Recuperando dados como um fluxo](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|Fornece uma visão geral de como transmitir dados do servidor e fornece links para casos de uso específicos.|  
|[Usando parâmetros direcionais](../../connect/php/using-directional-parameters.md)|Descreve como usar parâmetros direcionais ao chamar um procedimento armazenado.|  
|[Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|Demonstra como criar um conjunto de resultados com linhas que você pode acessar em qualquer ordem.|  
|[Como recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|Descreve como recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV.|  
|[Como recuperar tipos de data e hora como objetos Datetime PHP usando o driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)|Descreve como recuperar tipos de data e hora como objetos usando o driver PDO_SQLSRV.|  
|[Formatar cadeias de caracteres decimais com o Driver SQLSRV](../../connect/php/formatting-decimals-sqlsrv-driver.md)|Demonstra como formatar valores decimais ou monetários usando o driver SQLSRV.|  
|[Formatar cadeias de caracteres decimais com o Driver PDO_SQLSRV](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)|Demonstra como formatar valores decimais ou monetários usando o driver PDO_SQLSRV.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Como especificar tipos de dados do PHP](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Recuperando dados](../../connect/php/retrieving-data.md)  
  
