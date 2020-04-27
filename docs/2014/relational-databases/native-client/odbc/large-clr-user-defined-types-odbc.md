---
title: Tipos de CLR grandes definidos pelo usuário (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5af4f85652fc1a8a333912c741f96df014655ebe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63144298"
---
# <a name="large-clr-user-defined-types-odbc"></a>Tipos de dados CLR grandes definidos pelo usuário (ODBC)
  Este tópico aborda as alterações feitas ao ODBC no SQL Server Native Client para dar suporte aos UDTs (tipos definidos pelo usuário) de CLR (Common Language Runtime) grande.  
  
 Para obter um exemplo que mostra o suporte ODBC para UDTs CLR grandes, consulte [suporte para UDTs grandes](../../native-client-odbc-how-to/support-for-large-udts.md).  
  
 Para obter mais informações sobre o suporte a UDTs CLR grandes no SQL Server Native Client, consulte [grandes tipos CLR definidos pelo usuário](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="data-format"></a>Formato de Dados  
 O SQL Server Native Client usa SQL_SS_LENGTH_UNLIMITED para indicar que o tamanho de uma coluna é maior que 8.000 bytes para tipos LOB. A partir do SQL Server 2008, o mesmo valor é usado para UDTs do CLR quando seu tamanho for maior que 8.000 bytes.  
  
 Os valores UDT são representados como matrizes de bytes. Há suporte para conversões de cadeias hexadecimais e para cadeias hexadecimais. Os valores literais são representados como cadeias de caracteres hexadecimais com um prefixo "0x".  
  
 A seguinte tabela mostra o mapeamento de tipos de dados em parâmetros e conjuntos de resultados:  
  
|Tipo de dados do SQL Server|Tipo de dados SQL|Valor|  
|--------------------------|-------------------|-----------|  
|CLR UDT|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 A seguinte tabela discute a estrutura correspondente e o tipo do C do ODBC. Essencialmente, UDT do CLR é um tipo `varbinary` com metadados adicionais.  
  
|Tipo de dados SQL|Layout de memória|Tipos de dados do C|Valor (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (caractere \*não assinado)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>Campos do descritor dos parâmetros  
 As informações são retornadas nos campos IPD são as seguintes:  
  
|Campo do descritor|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema que contém o UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
 Para parâmetros UDT, SQL_CA_SS_UDT_TYPE_NAME sempre deve ser definido via **SQLSetDescField**. SQL_CA_SS_UDT_CATALOG_NAME e SQL_CA_SS_UDT_SCHEMA_NAME são opcionais.  
  
 Se o UDT for definido no mesmo banco de dados com um esquema diferente que a tabela, SQL_CA_SS_UDT_SCHEMA_NAME deve ser definido.  
  
 Se o UDT for definido em um banco de dados diferente da tabela, SQL_CA_SS_UDT_CATALOG_NAME e SQL_CA_SS_UDT_SCHEMA_NAME devem ser definidos.  
  
 Se houver quaisquer erros ou omissões nas definições de SQL_CA_SS_UDT_TYPE_NAME, SQL_CA_SS_UDT_CATALOG_NAME ou SQL_CA_SS_UDT_SCHEMA_NAME, é gerado um registro de diagnóstico com SQLSTATE HY000 e texto de mensagem específico do servidor.  
  
## <a name="descriptor-fields-for-results"></a>Campos do descritor dos resultados  
 As informações retornadas nos campos IRD são as seguintes:  
  
|Campo do descritor|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema que contém o UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)  
 Os seguintes valores de coluna são retornados para UDTs:  
  
|Nome da coluna|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULO|NULO|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULO|NULO|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
 As últimas três colunas são específicas do driver. Elas são adicionadas após qualquer coluna definida pelo ODBC, mas antes de qualquer coluna específica do driver existente do conjunto de resultados de SQLColumns ou SQLProcedureColumns.  
  
 Nenhuma linha é retornada por SQLGetTypeInfo, para UDTs individuais ou para o tipo genérico "UDT".  
  
## <a name="bindings-and-conversions"></a>Associações e conversões  
 As conversões de tipos de dados de C para SQL com suporte são as seguintes:  
  
|Conversão para e de:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Porta|  
|SQL_C_BINARY|Suportado|  
|SQL_C_CHAR|Porta|  
  
 \*Os dados binários são convertidos em uma cadeia de caracteres hexadecimal.  
  
 As conversões com suporte dos tipos de dados do C para SQL são as seguintes:  
  
|Conversão para e de:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Porta|  
|SQL_C_BINARY|Suportado|  
|SQL_C_CHAR|Porta|  
  
 \*A conversão de cadeia de caracteres hexadecimal para dados binárias ocorre.  
  
## <a name="sql_variant-support-for-udts"></a>Suporte SQL_VARIANT para UDTs  
 Não há suporte para UDTs em colunas de SQL_VARIANT.  
  
## <a name="bcp-support-for-udts"></a>Suporte BCP para UDTs  
 Valores de UDTs podem ser importados e exportados somente como valores de caracteres ou binários.  
  
## <a name="downlevel-client-behavior-for-udts"></a>Comportamento do cliente de baixo nível para UDTs  
 Os UDTs estão sujeitos ao mapeamento de tipo com clientes de baixo nível, conforme indicado a seguir:  
  
|Versão do servidor __|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|`UDT`|`varbinary(max)`|  
|SQL Server 2008 e posterior|`UDT`|`UDT`|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>Funções ODBC que dão suporte a UDTs de CLR grande  
 Esta seção discute as alterações feitas nas funções ODBC do SQL Server Native Client para dar suporte a UDTs de CLR grande.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Os valores de coluna de resultado UDT são convertidos de SQL para tipos de DataType, conforme descrito na seção "associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 Os valores necessários para UDTs são os seguintes:  
  
|Tipo de dados SQL|*ParameterType*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Os valores retornados para UDTs são os descritos na seção "Campos do descritor dos resultados", anteriormente neste tópico.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Os valores retornados para UDTs são conforme descrito na seção "metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 Os valores de coluna de resultado UDT são convertidos de SQL para tipos de DataType, conforme descrito na seção "associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Os valores de coluna de resultado UDT são convertidos de SQL para tipos de DataType, conforme descrito na seção "associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Os valores de coluna de resultado UDT são convertidos de SQL para tipos de DataType, conforme descrito na seção "associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 Os campos de descritor disponíveis como os novos tipos são descritos nas seções "Campos do descritor dos parâmetros" e "Campos do descritor dos resultados", anteriormente neste tópico.  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|Tipo|SubType|Comprimento|Precisão|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 Os valores retornados para UDTs são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 Os valores retornados para UDTs são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
### <a name="sqlputdata"></a>SQLPutData  
 Os valores de parâmetros UDT são convertidos de C para tipos de texto do SQL, conforme descrito na seção "associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 O campo de descritor disponível com os novos tipos é descrito nas seções "campos do descritor para parâmetros" e "campos do descritor para resultados", anteriormente neste tópico.  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 Os valores permitidos para UDTs são os seguintes:  
  
|Tipo de dados SQL|Tipo|SubType|Comprimento|Precisão|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 Os valores retornados para os UDTs das colunas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGITS são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados CLR grandes definidos pelo usuário](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
