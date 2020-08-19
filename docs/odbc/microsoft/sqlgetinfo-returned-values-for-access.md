---
description: Valores retornados SQLGetInfo para Access
title: SQLGetInfo retornou valores para acesso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- SQLGetInfo function [ODBC], Access Driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], SQLGetInfo
ms.assetid: c551e07f-30c4-41a2-8991-6010a3511d76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27af9272132b2e7f2489def0d1e6720bfdeb4195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421730"
---
# <a name="sqlgetinfo-returned-values-for-access"></a>Valores retornados SQLGetInfo para Access
A tabela a seguir lista os #defines de linguagem C para o argumento *fInfoType* e os valores correspondentes retornados por **SQLGetInfo**. Essas informações podem ser recuperadas passando o #defines de linguagem C listado para **SQLGetInfo** no argumento *fInfoType* . Para obter mais informações sobre os valores retornados por **SQLGetInfo**, consulte a *referência do programador de ODBC*.  
  
> [!NOTE]  
>  Onde **SQLGetInfo** retorna um bitmask de 32 bits, uma barra vertical (&#124;) representa uma ou bit-a-bit.  
  
|InfoType|Valor retornado|  
|--------------|--------------------|  
|SQL_ACCESSIBLE_PROCEDURES|"Y"|  
|SQL_ACCESSIBLE_TABLES|"Y"|  
|SQL_ACTIVE_ENVIRONMENTS|0|  
|SQL_AGGREGATE_FUNCTIONS|Todos os conjuntos|  
|SQL_ALTER_DOMAIN|0|  
|SQL_ALTER_TABLE|0|  
|SQL_ASYNC_MODE|0|  
|SQL_BATCH_ROW_COUNT|0|  
|SQL_BATCH_SUPPORT|0|  
|SQL_BOOKMARK_PERSISTENCE|Vários valores|  
|SQL_CATALOG_LOCATION|SQL_QL_START|  
|SQL_CATALOG_NAME|"Y"|  
|SQL_CATALOG_NAME_SEPARATOR|"."|  
|SQL_CATALOG_TERM|Banco|  
|SQL_CATALOG_USAGE|Vários valores|  
|SQL_COLLATION_SEQ|""|  
|SQL_COLUMN_ALIAS|"Y"|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_CB_NON_NULL|  
|SQL_CONVERT_BIGINT|0|  
|SQL_CONVERT_BINARY|Vários valores|  
|SQL_CONVERT_BIT|0|  
|SQL_CONVERT_CHAR|Vários valores|  
|SQL_CONVERT_DATE|Vários valores|  
|SQL_CONVERT_DECIMAL|0|  
|SQL_CONVERT_DOUBLE|Vários valores|  
|SQL_CONVERT_FLOAT|Vários valores|  
|SQL_CONVERT_FUNCTIONS|SQL_FN_CVT_CONVERT|  
|SQL_CONVERT_INTEGER|Vários valores|  
|SQL_CONVERT_LONGVARBINARY|Vários valores|  
|SQL_CONVERT_LONGVARCHAR|Vários valores|  
|SQL_CONVERT_NUMERIC|Vários valores|  
|SQL_CONVERT_REAL|Vários valores|  
|SQL_CONVERT_SMALLINT|Vários valores|  
|SQL_CONVERT_TIME|Vários valores|  
|SQL_CONVERT_TIMESTAMP|Vários valores|  
|SQL_CONVERT_TINYINT|Vários valores|  
|SQL_CONVERT_VARBINARY|Vários valores|  
|SQL_CONVERT_VARCHAR|Vários valores|  
|SQL_CORRELATION_NAME|SQL_CN_ANY|  
|SQL_CREATE_ASSERTION|0|  
|SQL_CREATE_CHARACTER_SET|0|  
|SQL_CREATE_COLLATION|0|  
|SQL_CREATE_DOMAIN|0|  
|SQL_CREATE_SCHEMA|0|  
|SQL_CREATE_TABLE|SQL_CT_CREATE_TABLE|  
|SQL_CREATE_TRANSLATION|0|  
|SQL_CREATE_VIEW|SQL_CV_CREATE_VIEW|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_DATA_SOURCE_NAME|O DSN do Odbc.ini ou "" se a palavra-chave do DRIVER for usada em Odbc.ini|  
|SQL_DATA_SOURCE_READ_ONLY|"N"|  
|SQL_DATABASE_NAME|Nome do arquivo|  
|SQL_DATETIME_LITERALS|0|  
|SQL_DBMS_NAME|ÀS|  
|SQL_DBMS_VER|Vários valores|  
|SQL_DDL_INDEX|Vários valores|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_TXN_READ_COMMITTED|  
|SQL_DESCRIBE_PARAMETER|0|  
|SQL_DRIVER_HDBC|Manipulado pelo Gerenciador de driver.|  
|SQL_DRIVER_HENV|Manipulado pelo Gerenciador de driver.|  
|SQL_DRIVER_HLIB|Manipulado pelo Gerenciador de driver.|  
|SQL_DRIVER_HSTMT|Manipulado pelo Gerenciador de driver.|  
|SQL_DRIVER_NAME|"OdbcJt32.dll"|  
|SQL_DRIVER_ODBC_VER|"3.51.0000"|  
|SQL_DRIVER_VER|"4, 0.*nnnn*" (*nnnn* especifica a data de compilação)|  
|SQL_DROP_ASSERTION|0|  
|SQL_DROP_CHARACTER_SET|0|  
|SQL_DROP_COLLATION|0|  
|SQL_DROP_DOMAIN|0|  
|SQL_DROP_SCHEMA|0|  
|SQL_DROP_TABLE|SQL_DT_DROP_TABLE|  
|SQL_DROP_TRANSLATION|0|  
|SQL_DROP_VIEW|SQL_DV_DROP_VIEW|  
|SQL_EXPRESSIONS_IN_ORDERBY|"Y"|  
|SQL_FILE_USAGE|SQL_FILE_CATALOG|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT|  
|SQL_GETDATA_EXTENSIONS|Vários valores|  
|SQL_GROUP_BY|SQL_GB_GROUP_BY_CONTAINS_SELECT|  
|SQL_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_IDENTIFIER_QUOTE_CHAR|" \` " (aspas posteriores)|  
|SQL_KEYWORDS|Vários valores|  
|SQL_LIKE_ESCAPE_CLAUSE|"N"|  
|SQL_MAX_BINARY_LITERAL_LEN|255|  
|SQL_MAX_CATALOG_NAME_LEN|66|  
|SQL_MAX_CHAR_LITERAL_LEN|255|  
|SQL_MAX_COLUMN_NAME_LEN|64|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|10|  
|SQL_MAX_COLUMNS_IN_INDEX|32|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|10|  
|SQL_MAX_COLUMNS_IN_SELECT|255|  
|SQL_MAX_COLUMNS_IN_TABLE|255|  
|SQL_MAX_CONCURRENT_ACTIVITIES|0|  
|SQL_MAX_CURSOR_NAME_LEN|64|  
|SQL_MAX_DRIVER_CONNECTIONS|64|  
|SQL_MAX_INDEX_SIZE|255|  
|SQL_MAX_PROCEDURE_NAME_LEN|64|  
|SQL_MAX_ROW_SIZE|2096|  
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|"N"|  
|SQL_MAX_SCHEMA_NAME_LEN|0|  
|SQL_MAX_STATEMENT_LEN|65000|  
|SQL_MAX_TABLE_NAME_LEN|64|  
|SQL_MAX_TABLES_IN_SELECT|16|  
|SQL_MAX_USER_NAME_LEN|0|  
|SQL_MULT_RESULT_SETS|"N"|  
|SQL_MULTIPLE_ACTIVE_TXN|"Y"|  
|SQL_NEED_LONG_DATA_LEN|"N"|  
|SQL_NON_NULLABLE_COLUMNS|SQL_NNC_NON_NULL|  
|SQL_NULL_COLLATION|SQL_NC_LOW|  
|SQL_NUMERIC_FUNCTIONS|Vários valores|  
|CONFORMIDADE SQL_ODBC_SAG_CLI_|SQL_OSCC_COMPLIANT|  
|SQL_ODBC_SQL_INTEGRITY|"N"|  
|SQL_ODBC_VER|Do Gerenciador de driver|  
|SQL_OJ_CAPABILITIES|Vários valores|  
|SQL_ORDER_BY_COLUMNS_IN_SELECT|"N"|  
|SQL_OUTER_JOINS|"Y"|  
|SQL_PROCEDURE_TERM|CONSULTÁ|  
|SQL_PROCEDURES|"Y"|  
|SQL_QUOTED_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_ROW_UPDATES|"N"|  
|SQL_SCHEMA_TERM|""|  
|SQL_SCHEMA_USAGE|0|  
|SQL_SCROLL_OPTIONS|Vários valores|  
|SQL_SEARCH_PATTERN_ESCAPE|"\\"|  
|SQL_SERVER_NAME|ÀS|  
|SQL_SPECIAL_CHARACTERS|"~ \` @#$%^& \* \_ -+= \\ } {" \' ;:?/><,.! \' [] &#124; "|  
|SQL_STRING_FUNCTIONS|Vários valores|  
|SQL_SUBQUERIES|Vários valores|  
|SQL_SYSTEM_FUNCTIONS|0|  
|SQL_TABLE_TERM|TABELA|  
|SQL_TIMEDATE_ADD_INTERVALS|0|  
|SQL_TIMEDATE_DIFF_INTERVALS|0|  
|SQL_TIMEDATE_FUNCTIONS|Vários valores|  
|SQL_TXN_CAPABLE|SQL_TC_ALL|  
|SQL_TXN_ISOLATION_OPTION|SQL_TXN_READ_COMMITTED|  
|SQL_UNION|Vários valores|  
|SQL_USER_NAME|ADM|
