---
title: PDO::getAttribute
description: Referência da API para a função PDO::getAttribute no Driver PDO_SQLSRV da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c81833ea-8b8a-459d-8f24-920098da994d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1f3e189441109a61aeda6b6b39a16aefe940797
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646736"
---
# <a name="pdogetattribute"></a>PDO::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera o valor de um atributo de PDO ou driver predefinido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDO::getAttribute ( $attribute )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$attribute*: um dos atributos com suporte. Consulte a seção Comentários para obter uma lista de atributos com suporte.  
  
## <a name="return-value"></a>Valor de retorno  
Em caso de êxito, retorna o valor de uma opção de conexão, um atributo de PDO predefinido ou um atributo de driver personalizado. Retorna null em caso de falha.  
  
## <a name="remarks"></a>Comentários  
A tabela a seguir contém a lista dos atributos com suporte.  
  
|Atributo|Processado por|Valores com suporte|Descrição|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|Especifica se os nomes de coluna devem usar maiúsculas ou minúsculas. PDO::CASE_LOWER força nomes de coluna com letras minúsculas, PDO::CASE_NATURAL deixa o nome da coluna conforme retornado pelo banco de dados e PDO::CASE_UPPER força nomes de coluna com letras maiúsculas.<br /><br />O padrão é PDO::CASE_NATURAL.<br /><br />Esse atributo também pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_CLIENT_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|Matriz de cadeia de caracteres|Descreve as versões do driver e das bibliotecas relacionadas. Retorna uma matriz com os seguintes elementos: versão do ODBC (*MajorVer*.*MinorVer*), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome e versão da DLL do Cliente Nativo, versão [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] (*MajorVer*.*MinorVer*.*BuildNumber*.*Revision*)|  
|PDO::ATTR_DEFAULT_STR_PARAM|PDO|PDO::PARAM_STR_CHAR<br /><br />PDO::PARAM_STR_NATL|Caso não esteja definido como PDO::PARAM_STR_CHAR, PDO::PARAM_STR_NATL retornará.|
|PDO::ATTR_DRIVER_NAME|PDO|String|Sempre retorna "sqlsrv".|  
|PDO::ATTR_DRIVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|String|Indica a versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] (*MajorVer*.*MinorVer*.*BuildNumber*.*Revision*)|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|Especifica como as falhas devem ser tratadas pelo driver.<br /><br />PDO::ERRMODE_SILENT (o padrão) define os códigos e as informações de erro.<br /><br />PDO::ERRMODE_WARNING gera um E_WARNING.<br /><br />PDO::ERRMODE_EXCEPTION gera uma exceção.<br /><br />Esse atributo também pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_ORACLE_NULLS|PDO|Consulte a documentação do PDO.|Consulte a documentação do PDO.|  
|PDO::ATTR_SERVER_INFO|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|Matriz de 3 elementos|Retorna o banco de dados atual, a versão do SQL Server e a instância do SQL Server.|  
|PDO::ATTR_SERVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|String|Indica a versão do SQL Server (*Major*.*Minor*.*BuildNumber*)|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|Consulte a documentação do PDO|Consulte a documentação do PDO.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 para o limite de memória do PHP.|Configura o tamanho do buffer que contém o conjunto de resultados de um cursor do lado do cliente.<br /><br />O padrão é 10.240 KB (10 MB).<br /><br />Para obter mais informações sobre os cursores do lado do cliente, veja [Tipos de cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|Especifica a execução direta ou preparada da consulta. Para obter mais informações, consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM|Especifica a codificação do conjunto de caracteres usada pelo driver para se comunicar com o servidor.<br /><br />O padrão é PDO::SQLSRV_ENCODING_UTF8.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Lida com buscas numéricas de colunas com tipos numéricos do SQL (bit, inteiro, smallint, tinyint, float ou real).<br /><br />Quando o sinalizador de opção de conexão ATTR_STRINGIFY_FETCHES está ativado, mesmo quando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver ativado, o valor retornado é uma cadeia de caracteres.<br /><br />Quando o tipo PDO retornado na coluna de associação for PDO_PARAM_INT, o valor de retorno de uma coluna de números inteiros é int, mesmo se SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver desativado.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|Número inteiro|Define o tempo limite da consulta em segundos.<br /><br />O padrão é 0, o que significa que o driver aguardará resultados indefinidamente.<br /><br />Números negativos não são permitidos.|  

  
O PDO processa alguns atributos predefinidos e requer que o driver processe outros. Todos os atributos personalizados e opções de conexão são tratados pelo driver. Um atributo ou opção de conexão sem suporte retorna null.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra o valor do atributo PDO::ATTR_ERRMODE, antes e depois de alterar seu valor.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
$attributes1 = array( "ERRMODE" );  
foreach ( $attributes1 as $val ) {  
     echo "PDO::ATTR_$val: ";  
     var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
}  
  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
$attributes1 = array( "ERRMODE" );  
foreach ( $attributes1 as $val ) {  
     echo "PDO::ATTR_$val: ";  
     var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
}  
  
// An example using PDO::ATTR_CLIENT_VERSION  
print_r($conn->getAttribute( PDO::ATTR_CLIENT_VERSION ));  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
