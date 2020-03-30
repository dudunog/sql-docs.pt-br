---
title: Membros de SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d99bf6118af71981ad2f45b5c7b722b458cc158c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970756"
---
# <a name="sqlserverpreparedstatement-members"></a>Membros de SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|Adiciona um conjunto de parâmetros ao lote de comandos deste objeto Statement.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Cancela a instrução SQL que está sendo executada por este objeto Statement.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|Esvazia a lista atual de comandos SQL do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|Limpa os valores de parâmetros atuais imediatamente.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Limpa todos os avisos que são relatados neste objeto Statement.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|Libera imediatamente o banco de dados e os recursos do JDBC do objeto Statement, em vez de aguardar que eles sejam liberados automaticamente.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|Executa a instrução SQL no objeto Statement, que pode ser qualquer tipo de instrução SQL.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|Executa a consulta SQL no objeto Statement e retorna o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerado pela consulta.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|Executa a instrução SQL no objeto Statement, que precisa ser uma instrução SQL INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) que produziu este objeto Statement.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a direção para efetuar fetch em linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados gerados com base no objeto Statement.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de linhas do conjunto de resultados que é o tamanho de fetch padrão para objetos do conjunto de resultados gerados do objeto Statement.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera todas as chaves geradas automaticamente criadas como resultado da execução do objeto Statement.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de bytes que podem ser retornados para valores de coluna de caractere e binários em um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) produzido por este objeto Statement.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de linhas que um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerado por este objeto Statement pode conter.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|Recupera um objeto [SQLServerResultSetMetaData Class](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) que contém informações sobre as colunas do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que será retornado quando o objeto Statement for executado.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Move para o próximo resultado do objeto Statement.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|Recupera o número, os tipos e as propriedades dos parâmetros deste objeto Statement.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de segundos que o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará pela execução do objeto Statement.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o resultado atual como um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a simultaneidade do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto Statement.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a suspensão do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto Statement.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o tipo de conjunto de resultados para objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados por este objeto Statement.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md),) Recupera o resultado atual como uma contagem de atualização.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o primeiro aviso informado por chamadas neste objeto Statement.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Indica se o objeto Statement foi fechado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|Indica se o objeto da instrução é um wrapper para a interface especificada.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto Array fornecido.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto InputStream fornecido.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto BigDecimal fornecido.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o fluxo de entrada especificado.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Blob especificado.|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **Boolean** especificado.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **byte** especificado.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como a matriz de bytes especificada.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Reader especificado.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Clob fornecido.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o nome do cursor SQL como a Cadeia de Caracteres especificada que será usada por métodos de execução subsequentes.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de data especificado.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|Define o valor da coluna especificada para o valor da [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md).|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **double** especificado.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o modo de processamento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **float** especificado.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **int** especificado.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **long** especificado.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de bytes em uma coluna [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que armazena caracteres ou valores binários, como o número de bytes fornecido.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de linhas que qualquer objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) pode conter como o número fornecido.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Reader especificado.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto especificado.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como um valor nulo, considerando o tipo de parâmetro a ser definido.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|Define o parâmetro designado como o objeto **String** especificado.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|Define o valor do parâmetro designado usando o objeto fornecido.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Solicita que uma instrução seja colocada ou não em pool. Por padrão, um objeto SQLServerPreparedStatement pode ser colocado em pool quando criado.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o número de segundos que o driver aguardará pela execução de um objeto Statement como o número de segundos especificado.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Ref especificado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) como **String full** ou **adaptive** que não diferencia maiúsculas de minúsculas.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **short** especificado.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor **String** especificado.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto **SQLXML** especificado.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de hora especificado.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de carimbo de data/hora especificado.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|Define o número de parâmetro designado como o fluxo de entrada especificado, que terá o número de bytes indicado.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de URL especificado.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancele, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
