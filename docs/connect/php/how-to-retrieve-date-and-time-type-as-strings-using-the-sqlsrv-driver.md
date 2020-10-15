---
title: Recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV
description: Saiba como recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2dd1bd53b5ce3304b48fe8ed022e538d4d705154
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081435"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>Como recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ao usar o driver SQLSRV para o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você pode recuperar tipos de data e hora (**smalldatetime**, **datetime**, **date**, **time**, **datetime2** e **datetimeoffset**) como cadeias de caracteres especificando a seguinte opção na cadeia de conexão ou no nível de instrução:

```
'ReturnDatesAsStrings'=>true
```

O padrão é **false**, o que significa que os tipos **smalldatetime**, **datetime**, **date**, **time**, **datetime2** e **dateTimeOffset** serão retornados como objetos [Datetime do PHP](http://php.net/manual/en/class.datetime.php). Se essa opção for definida no nível de instrução, ela substituirá a configuração de nível de conexão.

O driver PDO_SQLSRV retorna tipos de data e hora como cadeias de caracteres por padrão. Para recuperá-los como objetos DateTime de PHP, confira [Como recuperar tipos de data e hora como objetos datetime PHP usando o PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)

## <a name="example-1"></a>Exemplo 1
O exemplo a seguir mostra a sintaxe especificando a recuperação dos tipos de data e hora como cadeias de caracteres.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_close($conn);
?>
```

## <a name="example-2"></a>Exemplo 2
O exemplo a seguir mostra que você pode recuperar datas como cadeias de caracteres especificando UTF-8 quando recuperar a cadeia de caracteres, mesmo quando a conexão tiver sido feita com `"ReturnDatesAsStrings" => false`.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;

sqlsrv_close($conn);
?>
```

## <a name="example-3"></a>Exemplo 3
O exemplo a seguir mostra como recuperar datas como cadeias de caracteres especificando UTF-8 e `"ReturnDatesAsStrings" => true` na cadeia de conexão.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8');
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;
sqlsrv_close($conn);
?>
```

## <a name="example-4"></a>Exemplo 4
O exemplo a seguir mostra como recuperar a data como um tipo do PHP. `'ReturnDatesAsStrings'=> false` está ativado por padrão.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as a DateTime object, then convert to string using PHP's date_format function
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

$date_string = date_format($date, 'jS, F Y');
echo "Date = $date_string\n";

sqlsrv_close($conn);
?>
```

## <a name="example-5"></a>Exemplo 5
A opção ReturnDatesAsStrings no nível de instrução substitui a opção de conexão correspondente.

```php
<?php
$serverName = 'MyServer';
$connectionInfo = array('Database' => 'MyDatabase', 'ReturnDatesAsStrings' => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tableName = 'MyTable';
$options = array('ReturnDatesAsStrings' => true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}
sqlsrv_execute($stmt);

// Expect the fetched value to be a string
$field = sqlsrv_get_field($stmt, 0);
echo $field . PHP_EOL;

sqlsrv_close($conn);
?>
```

## <a name="see-also"></a>Consulte Também
[Recuperando dados](../../connect/php/retrieving-data.md)

[Como recuperar tipos de data e hora como objetos datetime PHP usando o PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)
