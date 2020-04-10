---
title: Constantes (Drivers da Microsoft para PHP para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c54021d6165d0fbf221c7af1c4f10235efb55820
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928077"
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>Constantes (Drivers da Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico discute as constantes definidas pelos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="pdo_sqlsrv-driver-constants"></a>Constantes do driver PDO_SQLSRV  
As constantes listadas no [site de PDO](https://php.net/manual/book.pdo.php) são válidas nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
A seguir está a descrição das constantes específicas da Microsoft no driver PDO_SQLSRV.  
  
### <a name="transaction-isolation-level-constants"></a>Constantes de nível de isolamento de transação  
A chave **TransactionIsolation** , que é usada com [PDO::__construct](../../connect/php/pdo-construct.md), aceita uma das seguintes constantes:  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
Para obter mais informações sobre a chave **TransactionIsolation** , consulte [Connection Options](../../connect/php/connection-options.md).  
  
### <a name="encoding-constants"></a>Constantes de codificação  
O atributo PDO::SQLSRV_ATTR_ENCODING pode ser passado para [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md), [PDO::prepare](../../connect/php/pdo-prepare.md), [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) e [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md).  
  
Os valores disponíveis para passar para PDO::SQLSRV_ATTR_ENCODING são  
  
|Constante do driver PDO_SQLSRV|DESCRIÇÃO|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|Os dados são um fluxo de bytes brutos do servidor sem realizar a codificação ou a conversão.<br /><br />Não é válido para PDO::setAttribute.|  
|PDO::SQLSRV_ENCODING_SYSTEM|Os dados são caracteres de 8 bits conforme especificado na página de código da localidade do Windows definida no sistema. Todos os caracteres multibyte ou caracteres não mapeados nessa página de código são substituídos por um caractere de ponto de interrogação (?) de byte único.|  
|PDO::SQLSRV_ENCODING_UTF8|Os dados estão na codificação UTF-8. Essa é a codificação padrão.|  
|PDO::SQLSRV_ENCODING_DEFAULT|Usa PDO::SQLSRV_ENCODING_SYSTEM se especificado durante a conexão.<br /><br />Use a codificação da conexão se for especificado em uma instrução prepare.|  
  
### <a name="query-timeout"></a>Tempo-limite da consulta  
O atributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT é qualquer inteiro não negativo que representa o período limite, em segundos. Zero (0) é o padrão e significa sem tempo limite.  
  
Você pode especificar o atributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT com [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md) e [PDO::prepare](../../connect/php/pdo-prepare.md).  
  
### <a name="direct-or-prepared-execution"></a>Execução direta ou preparada  
Você pode selecionar a execução de consulta direta ou execução de instrução preparada com o atributo PDO::SQLSRV_ATTR_DIRECT_QUERY. PDO::SQLSRV_ATTR_DIRECT_QUERY pode ser definido com [PDO::prepare](../../connect/php/pdo-prepare.md) ou [PDO::setAttribute](../../connect/php/pdo-setattribute.md). Para obter mais informações sobre PDO::SQLSRV_ATTR_DIRECT_QUERY, veja [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  

### <a name="handling-numeric-fetches"></a>Lidando com buscas numéricas
O atributo PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE pode ser usado para manipular buscas numéricas de colunas com tipos SQL numéricos (bit, integer, smallint, tinyint, float e real). Quando PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE é definido como true, os resultados de uma coluna do tipo integer são representados como ints, enquanto valores do SQL dos tipos float e real são representados como floats. Este atributo pode ser definido com [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). 

Você pode modificar o comportamento padrão de formatação de decimais com os atributos PDO::SQLSRV_ATTR_FORMAT_DECIMALS e PDO::SQLSRV_ATTR_DECIMAL_PLACES. O comportamento desses atributos é idêntico às opções correspondentes no lado do SQLSRV (**FormatDecimals** e **DecimalPlaces**), exceto pelo fato de que o uso de parâmetros de saída para formatação não é compatível. Esses atributos podem ser definidos no nível da conexão ou da instrução, com [PDO::setAttribute](../../connect/php/pdo-setattribute.md) ou [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), mas qualquer atributo de instrução substituirá o atributo de conexão correspondente. Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).

### <a name="handling-date-and-time-fetches"></a>Como processar buscas de data e hora

O PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE Especifica quando recuperar tipos de data e hora como objetos [DateTime do PHP](http://php.net/manual/en/class.datetime.php). Se for deixado como false, o comportamento padrão será retorná-los como cadeias de caracteres. Esse atributo podem ser definidos no nível da conexão ou da instrução, com [PDO::setAttribute](../../connect/php/pdo-setattribute.md) ou [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), mas o atributo de instrução substituirá o atributo de conexão correspondente. Para saber mais, confira [Como recuperar tipos de data e hora como objetos DateTime PHP usando o driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).

## <a name="sqlsrv-driver-constants"></a>SQLSRV  
As seções a seguir listam as constantes usadas pelo driver SQLSRV.  
  
### <a name="err-constants"></a>Constantes ERR  
A tabela a seguir lista as constantes usadas para especificar se [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) retorna erros, avisos ou ambos.  
  
|Valor|DESCRIÇÃO|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Retorna erros e avisos gerados na última chamada da função **sqlsrv** . Esse é o valor padrão.|  
|SQLSRV_ERR_ERRORS|Retorna erros gerados na última chamada da função **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Retorna avisos gerados na última chamada da função **sqlsrv** .|  
  
### <a name="fetch-constants"></a>Constantes FETCH  
A tabela a seguir lista as constantes usadas para especificar o tipo de matriz retornada por [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
|Constante SQLSRV|DESCRIÇÃO|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** retorna a próxima linha de dados como matriz associativa.|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** retorna a próxima linha de dados como matriz com as chaves numéricas e associativas. Esse é o valor padrão.|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** retorna a próxima linha de dados como matriz numericamente indexada.|  
  
### <a name="logging-constants"></a>Constantes de registro em log  
Esta seção lista as constantes usadas para alterar as configurações de registro em log com [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). Para obter mais informações sobre o registro de atividades em log, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
A tabela a seguir apresenta as constantes que podem ser usadas como o valor para a configuração **LogSubsystems** :  
  
|Constante SQLSRV (inteiro equivalente entre parênteses)|DESCRIÇÃO|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Ativa o registro em log de todos os subsistemas.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Ativa o registro em log da atividade de conexão.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Ativa o registro em log da atividade de inicialização.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Desativa o registro em log.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Ativa o registro em log da atividade de instrução.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Ativa o registro em log da atividade de funções de erro (como **handle_error** e **handle_warning**).|  
  
A tabela a seguir apresenta as constantes que podem ser usadas como o valor para a configuração **LogSeverity** :  
  
|Constante SQLSRV (inteiro equivalente entre parênteses)|DESCRIÇÃO|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Especifica que erros, avisos e notificações serão registrados em log.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Especifica que os erros serão registrados em log.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Especifica que as notificações serão registradas em log.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Especifica que os avisos serão registrados em log.|  
  
### <a name="nullable-constants"></a>Constantes que permitem valor nulo  
A tabela a seguir lista as constantes que você pode usar para determinar se uma coluna permite ou não valor nulo ou se essas informações não estão disponíveis. Você pode comparar o valor da chave **Nullable** retornada por [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) para determinar o status da coluna que permite valor nulo.  
  
|Constante SQLSRV (inteiro equivalente entre parênteses)|DESCRIÇÃO|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|A coluna permite valor nulo.|  
|SQLSRV_NULLABLE_NO (1)|A coluna não permite valor nulo.|  
|SQLSRV_NULLABLE_UNKNOWN (2)|Não se sabe se a coluna permite valor nulo.|  
  
### <a name="param-constants"></a>Constantes PARAM  
A lista a seguir contém as constantes para especificar a direção do parâmetro ao chamar [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
|Constante SQLSRV|DESCRIÇÃO|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|Indica um parâmetro de entrada.|  
|SQLSRV_PARAM_INOUT|Indica um parâmetro bidirecional.|  
|SQLSRV_PARAM_OUT|Indica um parâmetro de saída.|  
  
### <a name="phptype-constants"></a>Constantes PHPTYPE  
A tabela a seguir apresenta as constantes usadas para descrever tipos de dados do PHP. Para obter informações sobre tipos de dados do PHP, veja [Tipos do PHP](https://php.net/manual/en/language.types.php).  
  
|Constante SQLSRV|Tipo de dados do PHP|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Integer|  
|SQLSRV_PHPTYPE_DATETIME|Datetime|  
|SQLSRV_PHPTYPE_FLOAT|Float|  
|SQLSRV_PHPTYPE_STREAM($encoding<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING($encoding<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** e **SQLSRV_PHPTYPE_STRING** aceitam um parâmetro que especifica a codificação do fluxo. A tabela a seguir contém as constantes SQLSRV que são parâmetros aceitáveis e uma descrição da codificação correspondente.  
  
|Constante SQLSRV|DESCRIÇÃO|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|Os dados são retornados do servidor como um fluxo de bytes brutos, sem codificação ou conversão.|  
|SQLSRV_ENC_CHAR|Os dados são retornados em caracteres de 8 bits conforme especificado na página de código da localidade do Windows definida no sistema. Todos os caracteres multibyte ou caracteres não mapeados nessa página de código são substituídos por um caractere de ponto de interrogação (?) de byte único.<br /><br />Essa é a codificação padrão.|  
|"UTF-8"|Os dados são retornados na codificação UTF-8. Esta constante foi adicionada na versão 1.1 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Para obter mais informações sobre o suporte a UTF-8, veja [Como enviar e recuperar dados UTF-8 usando o suporte interno a UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|  
  
> [!NOTE]  
> Quando você usa **SQLSRV_PHPTYPE_STREAM** ou **SQLSRV_PHPTYPE_STRING**, a codificação deve ser especificada. Se nenhum parâmetro for fornecido, um erro será retornado.  
  
Para obter mais informações sobre essas constantes, consulte [Como especificar tipos de dados do PHP](../../connect/php/how-to-specify-php-data-types.md), [Como recuperar dados de caractere como um fluxo usando o driver SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md).  
  
### <a name="sqltype-constants"></a>Constantes SQLTYPE  
A tabela a seguir apresenta as constantes usadas para descrever tipos de dados do SQL Server. Algumas constantes são semelhantes a funções e podem usar parâmetros correspondentes a precisão, escala e/ou comprimento.  Ao associar parâmetros, deve-se usar as constantes semelhantes a funções. Para comparações de tipo, as constantes padrão (não semelhantes a funções) são necessárias. Para obter informações sobre tipos de dados do SQL Server, veja [Tipos de dados (Transact-SQL).](../../t-sql/data-types/data-types-transact-sql.md) Para obter informações sobre precisão, escala e comprimento, veja [Precisão, escala e comprimento (Transact-SQL).](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
|Constante SQLSRV|Tipo de dados do SQL Server|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|BIGINT|  
|SQLSRV_SQLTYPE_BINARY|binary|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|DATETIME|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|decimal<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|decimal|  
|SQLSRV_SQLTYPE_FLOAT|FLOAT|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|INT|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|numeric<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|numeric|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|NVARCHAR|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|real|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|SMALLINT|  
|SQLSRV_SQLTYPE_SMALLMONEY|SMALLMONEY|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|timestamp|  
|SQLSRV_SQLTYPE_TINYINT|TINYINT|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|  
|SQLSRV_SQLTYPE_UDT|UDT|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|Xml|  
  
1.  Esse é um tipo herdado que é mapeado para o tipo varbinary(max).  
  
2.  Esse é um tipo herdado que é mapeado para o tipo nvarchar mais recente.  
  
3.  Esse é um tipo herdado que é mapeado para o tipo varchar mais recente.  
  
4.  Foi adicionado suporte para esse tipo na versão 1.1 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

5.  Essas constantes devem ser usadas em operações de comparação de tipos e não substituem as constantes similares a funções com sintaxe semelhante. Ao associar parâmetros, deve-se usar as constantes semelhantes a funções.

  
A tabela a seguir lista as constantes SQLTYPE que aceitam parâmetros e o intervalo de valores permitido para o parâmetro.  
  
|SQLTYPE|Parâmetro|Intervalo permitido para o parâmetro|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1 - 8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1 - 4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1 - 8000|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|precisão|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|scale|1 - precisão|  
  
### <a name="transaction-isolation-level-constants"></a>Constantes de nível de isolamento de transação  
A chave **TransactionIsolation** , que é usada com [sqlsrv_connect](../../connect/php/sqlsrv-connect.md), aceita uma das seguintes constantes:  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>Cursor e constantes de rolagem  
As constantes a seguir especificam o tipo de cursor que pode ser usado em um conjunto de resultados:  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
As seguintes constantes especificam quais linhas selecionar no conjunto de resultados:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obter informações sobre como usar essas constantes, consulte [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
