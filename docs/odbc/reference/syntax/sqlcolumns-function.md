---
title: Função SQLColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301252"
---
# <a name="sqlcolumns-function"></a>Função SQLColumns
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: abrir grupo  
  
 **Resumo**  
 **SQLColumns** retorna a lista de nomes de coluna em tabelas especificadas. O driver retorna essas informações como um conjunto de resultados no *StatementHandle*especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *CatalogName*  
 Entrada Nome do catálogo. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de esquema. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm esquemas.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de tabela.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **TableName*.  
  
 *ColumnName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de coluna.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ColumnName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ColumnName* será um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength4*  
 Entrada Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColumns** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle* , mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName*, *TableName*ou *ColumnName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLColumns** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento do nome era menor que 0, mas não é igual a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o catálogo ou nome correspondente. O comprimento máximo de cada catálogo ou nome pode ser obtido chamando **SQLGetInfo** com os valores *InfoType* . (Consulte "Comentários".)|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um nome de catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um nome de esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o nome do esquema, o nome da tabela ou o nome da coluna, e a fonte de dados não oferece suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Normalmente, essa função é usada antes da execução da instrução para recuperar informações sobre colunas de uma tabela ou tabelas do catálogo da fonte de dados. **SQLColumns** pode ser usado para recuperar dados para todos os tipos de itens retornados por **SQLTables**. Além das tabelas base, isso pode incluir (mas não está limitado a) exibições, sinônimos, tabelas do sistema e assim por diante. Por outro lado, as funções **SQLColAttribute** e **SQLDescribeCol** descrevem as colunas em um conjunto de resultados e a função **SQLNumResultCols** retorna o número de colunas em um conjunto de resultados. Para obter mais informações, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLColumns** retorna os resultados como um conjunto de resultados padrão, ordenados por TABLE_CAT, TABLE_SCHEM, TABLE_NAME e ORDINAL_POSITION.  
  
> [!NOTE]  
>  Quando um aplicativo funciona com um ODBC 2. *x* , nenhuma coluna de ORDINAL_POSITION é retornada no conjunto de resultados. Como resultado, ao trabalhar com ODBC 2. drivers *x* , a ordem das colunas na lista de colunas retornada por **SQLColumns** não é necessariamente igual à ordem das colunas retornadas quando o aplicativo executa uma instrução SELECT em todas as colunas nessa tabela.  
  
> [!NOTE]  
>  **SQLColumns** pode não retornar todas as colunas. Por exemplo, um driver pode não retornar informações sobre as pseudovariáveis, como o ROWID da Oracle. Os aplicativos podem usar qualquer coluna válida, seja ela retornada por **SQLColumns**.  
>   
>  Algumas colunas que podem ser retornadas por **SQLStatistics** não são retornadas por **SQLColumns**. Por exemplo, **SQLColumns** não retorna as colunas em um índice criado em uma expressão ou filtro, como salário + benefícios ou Dept = 0012.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As colunas a seguir foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|ODBC 3. coluna *x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 As colunas a seguir foram adicionadas ao conjunto de resultados retornado por **SQLColumns** para ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 18 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas de driver, contando a partir do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Coluna<br /><br /> número|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1,0)|1|Varchar|Nome do catálogo; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1,0)|2|Varchar|Nome do esquema; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1,0)|3|Varchar não nulo|Nome da tabela.|  
|COLUMN_NAME (ODBC 1,0)|4|Varchar não nulo|Nome da coluna. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1,0)|5|Smallint não NULL|Tipo de dados SQL. Pode ser um tipo de dados ODBC do SQL ou um tipo de dados SQL específico do driver. Para os tipos de dados DateTime e Interval, essa coluna retorna o tipo de dados conciso (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH, em vez do tipo de dados não conciso, como SQL_DATETIME ou SQL_INTERVAL). Para obter uma lista de tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.<br /><br /> Os tipos de dados retornados para ODBC 3. *x* e ODBC 2. os aplicativos *x* podem ser diferentes. Para obter mais informações, consulte [compatibilidade com versões anteriores e conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1,0)|6|Varchar não nulo|Nome do tipo de dados dependente de fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" ou "CHAR () para dados de BIT".|  
|COLUMN_SIZE (ODBC 1,0)|7|Integer|Se DATA_TYPE for SQL_CHAR ou SQL_VARCHAR, essa coluna conterá o comprimento máximo em caracteres da coluna. Para tipos de dados DateTime, este é o número total de caracteres necessários para exibir o valor quando ele é convertido em caracteres. Para tipos de dados numéricos, esse é o número total de dígitos ou o número total de bits permitidos na coluna, de acordo com a coluna de NUM_PREC_RADIX. Para tipos de dados de intervalo, esse é o número de caracteres na representação de caractere do literal de intervalo (conforme definido pela precisão inicial do intervalo, consulte [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) no Apêndice D: tipos de dados). Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|BUFFER_LENGTH (ODBC 1,0)|8|Integer|O comprimento em bytes de dados transferidos em uma operação SQLGetData, SQLFetch ou SQLFetchScroll se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do tamanho dos dados armazenados na fonte de dados. Esse valor pode ser diferente de COLUMN_SIZE coluna para dados de caractere. Para obter mais informações sobre comprimento, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|DECIMAL_DIGITS (ODBC 1,0)|9|Smallint|O número total de dígitos significativos à direita do ponto decimal. Para SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, essa coluna contém o número de dígitos no componente de segundos fracionários. Para os outros tipos de dados, esses são os dígitos decimais da coluna na fonte de dados. Para tipos de dados de intervalo que contêm um componente de tempo, essa coluna contém o número de dígitos à direita do ponto decimal (segundos fracionários). Para tipos de dados de intervalo que não contêm um componente de tempo, essa coluna é 0. Para obter mais informações sobre dígitos decimais, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados. NULL é retornado para os tipos de dados em que DECIMAL_DIGITS não é aplicável.|  
|NUM_PREC_RADIX (ODBC 1,0)|10|Smallint|Para tipos de dados numéricos, 10 ou 2. Se for 10, os valores em COLUMN_SIZE e DECIMAL_DIGITS fornecerão o número de dígitos decimais permitidos para a coluna. Por exemplo, uma coluna DECIMAL (12, 5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e uma DECIMAL_DIGITS de 5; uma coluna FLOAT pode retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 15 e uma DECIMAL_DIGITS de NULL.<br /><br /> Se for 2, os valores em COLUMN_SIZE e DECIMAL_DIGITS fornecerão o número de bits permitidos na coluna. Por exemplo, uma coluna FLOAT poderia retornar uma RADIX de 2, uma COLUMN_SIZE de 53 e uma DECIMAL_DIGITS de NULL.<br /><br /> NULL é retornado para os tipos de dados em que NUM_PREC_RADIX não é aplicável.|  
|NULLABLE (ODBC 1,0)|11|Smallint não NULL|SQL_NO_NULLS se a coluna não pode incluir valores nulos.<br /><br /> SQL_NULLABLE se a coluna aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN se não for conhecido se a coluna aceita valores nulos.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para a coluna IS_NULLABLE. A coluna ANULÁVEL indica com certeza que uma coluna pode aceitar nulos, mas não pode indicar com certeza que uma coluna não aceita nulos. A coluna IS_NULLABLE indica com certeza que uma coluna não pode aceitar nulos, mas não pode indicar com certeza que uma coluna aceita nulos.|  
|COMENTÁRIOS (ODBC 1,0)|12|Varchar|Uma descrição da coluna.|  
|COLUMN_DEF (ODBC 3,0)|13|Varchar|O valor padrão da coluna. O valor nessa coluna deve ser interpretado como uma cadeia de caracteres se estiver entre aspas.<br /><br /> Se NULL tiver sido especificado como o valor padrão, essa coluna será a palavra NULL, não colocada entre aspas. Se o valor padrão não puder ser representado sem truncamento, essa coluna conterá TRUNCAdo, sem colocar aspas simples. Se nenhum valor padrão tiver sido especificado, essa coluna será nula.<br /><br /> O valor de COLUMN_DEF pode ser usado na geração de uma nova definição de coluna, exceto quando ele contém o valor TRUNCAdo.|  
|SQL_DATA_TYPE (ODBC 3,0)|14|Smallint não NULL|Tipo de dados SQL, como aparece no campo de registro SQL_DESC_TYPE no IRD. Pode ser um tipo de dados ODBC do SQL ou um tipo de dados SQL específico do driver. Essa coluna é igual à DATA_TYPE coluna, exceto para os tipos de dados DateTime e Interval. Essa coluna retorna o tipo de dados não conciso (como SQL_DATETIME ou SQL_INTERVAL), em vez do tipo de dados conciso (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH) para os tipos de dados DateTime e Interval. Se essa coluna retornar SQL_DATETIME ou SQL_INTERVAL, o tipo de dados específico poderá ser determinado a partir da coluna SQL_DATETIME_SUB. Para obter uma lista de tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.<br /><br /> Os tipos de dados retornados para ODBC 3. *x* e ODBC 2. os aplicativos *x* podem ser diferentes. Para obter mais informações, consulte [compatibilidade com versões anteriores e conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|SQL_DATETIME_SUB (ODBC 3,0)|15|Smallint|O código de subtipo para tipos de dados DateTime e Interval. Para outros tipos de dados, essa coluna retorna um valor nulo. Para obter mais informações sobre os subcódigos DateTime e Interval, consulte "SQL_DESC_DATETIME_INTERVAL_CODE" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3,0)|16|Integer|O comprimento máximo em bytes de uma coluna de tipo de dados binary ou de caractere. Para todos os outros tipos de dados, essa coluna retorna um valor nulo.|  
|ORDINAL_POSITION (ODBC 3,0)|17|Integer não NULL|A posição ordinal da coluna na tabela. A primeira coluna na tabela é o número 1.|  
|IS_NULLABLE (ODBC 3,0)|18|Varchar|"Não" se a coluna não incluir valores nulos.<br /><br /> "Sim" se a coluna puder incluir nulos.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para a coluna que permite valor nulo. (Consulte a descrição da coluna ANULÁVEL.)|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo declara buffers para o conjunto de resultados retornado por **SQLColumns**. Ele chama **SQLColumns** para retornar um conjunto de resultados que descreve cada coluna na tabela Employee. Em seguida, ele chama **SQLBindCol** para associar as colunas no conjunto de resultados aos buffers. Por fim, o aplicativo busca cada linha de dados com **SQLFetch** e processa-a.  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando colunas que identificam exclusivamente uma linha ou colunas automaticamente atualizadas por uma transação|[Função SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Retornando índices e estatísticas de tabela|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando uma lista de tabelas em uma fonte de dados|[Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Retornando privilégios para uma tabela ou tabelas|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
