---
title: Rastrear a operação do driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb926c0696f0e926f91297ee5b719bbafce3eda8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909112"
---
# <a name="tracing-driver-operation"></a>Rastreamento de operação do driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível com o uso de rastreamento (ou log) para ajudar a resolver problemas com o driver JDBC quando ele é usado em seu aplicativo. Para habilitar o uso de rastreamento, o driver JDBC usa as APIs de log no java.util.logging, que fornece um conjunto de classes para criar objetos Logger e LogRecord.  
  
> [!NOTE]  
>  Para o componente nativo (sqljdbc_xa.dll) que está incluído com o driver JDBC, o rastreamento é habilitado pela estrutura de Diagnósticos Internos (BID). Para obter mais informações sobre BID, consulte [Rastreamento do acesso a dados no SQL Server](https://go.microsoft.com/fwlink/?LinkId=70042).  
  
 Quando você desenvolve seu aplicativo, pode fazer chamadas para objetos Logger, que, por sua vez, criam objetos LogRecord, que serão então passados aos objetos Handler para processamento. Ambos os objetos Logger e Handler usam níveis de log e, opcionalmente, filtros de log para regulamentar quais LogRecords são processados. Quando as operações de log estiverem concluídas, os objetos Handler poderão usar objetos Formatter como opção para publicar as informações de log.  
  
 Por padrão, a estrutura do java.util.logging grava sua saída em um arquivo. Este arquivo de log de saída deve ter permissões de gravação para o contexto sob o qual o driver JDBC está executando.  
  
> [!NOTE]  
>  Para obter mais informações sobre como usar os vários objetos de log para rastreamento de programa, consulte a documentação do Java Logging APIs no site da Sun Microsystems.  
  
 As seções a seguir descrevem os níveis de log e as categorias que podem ser registradas em log, e fornecem informações sobre como habilitar rastreamento em seu aplicativo.  
  
## <a name="logging-levels"></a>Níveis de log  
 Toda mensagem de log que é criada tem um nível de log associado. O nível de registro em log determina a importância da mensagem de log, que é definida pela classe **Level** em java.util.logging. Habilitar log em um nível também habilita log em todos os níveis mais altos. Esta seção descreve os níveis de log para categorias de log públicas e categorias de log internas. Para saber mais sobre categorias de log, consulte a seção Categorias de log neste artigo.  
  
 A tabela a seguir descreve cada nível de log disponível para categorias de log públicas.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|SEVERE|Indica uma falha séria e é o nível mais alto de log. No driver JDBC, este nível é usado para relatar erros e exceções.|  
|WARNING|Indica um problema potencial.|  
|INFO|Fornece mensagens informativas.|  
|CONFIG|Fornece mensagens de configuração. Observe que o driver JDBC atualmente não fornece nenhuma mensagem de configuração.|  
|FINE|Fornece informações básicas de rastreamento inclusive todas as exceções lançadas pelos métodos públicos.|  
|FINER|Fornece informações de rastreamento detalhadas inclusive todas as entradas de método público e pontos de saída com tipos de dados de parâmetro associados e todas as propriedades públicas para classes públicas. Além disso, os parâmetros de entrada, os parâmetros de saída e o método retornam valores, exceto os tipos de valores retornados CLOB, BLOB, NCLOB, Reader, \<stream>.|  
|FINEST|Fornece informações de rastreamento altamente detalhadas. Este é o nível mais baixo de log.|  
|OFF|Desliga o log.|  
|ALL|Habilita log de todas as mensagens.|  
  
 A tabela a seguir descreve cada nível de log disponível para as categorias de log internas.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|SEVERE|Indica uma falha séria e é o nível mais alto de log. No driver JDBC, este nível é usado para relatar erros e exceções.|  
|WARNING|Indica um problema potencial.|  
|INFO|Fornece mensagens informativas.|  
|FINE|Fornece informações de rastreamento que incluem criação e destruição básicas de objeto. Além disso, todas as exceções lançadas pelos métodos públicos.|  
|FINER|Fornece informações de rastreamento detalhadas inclusive todas as entradas de método público e pontos de saída com tipos de dados de parâmetro associados e todas as propriedades públicas para classes públicas. Além disso, os parâmetros de entrada, os parâmetros de saída e o método retornam valores, exceto os tipos de valores retornados CLOB, BLOB, NCLOB, Reader, \<stream>.<br /><br /> As categorias de log a seguir existiam na versão 1.2 do driver JDBC e tinham o nível de log FINE: [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA e [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Desde a versão 2.0, estes são atualizados para o nível FINER.|  
|FINEST|Fornece informações de rastreamento altamente detalhadas. Este é o nível mais baixo de log.<br /><br /> As categorias de log a seguir existiam na versão 1.2 do driver JDBC e tinham o nível de log FINEST: TDS.DATA e TDS.TOKEN. Desde a versão 2.0, eles mantêm o nível de log FINEST.|  
|OFF|Desliga o log.|  
|ALL|Habilita log de todas as mensagens.|  
  
## <a name="logging-categories"></a>Categorias de log  
 Ao criar um objeto Logger, você deve dizer a ele sobre qual entidade ou categoria nomeada você está interessado em obter informações de log. O driver JDBC suporta as categorias de log públicas a seguir, que estão todas definidas no pacote do driver com.microsoft.sqlserver.jdbc.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|Conexão|Registra em log mensagens na classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Os aplicativos podem definir o nível de log como FINER.|  
|de|Registra em log mensagens na classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Os aplicativos podem definir o nível de log como FINER.|  
|DataSource|Registra mensagens em log na classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|ResultSet|Registra em log mensagens na classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Os aplicativos podem definir o nível de log como FINER.|  
|Driver|Registra em log mensagens na classe [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md). Os aplicativos podem definir o nível de log como FINER.|  
  
 A partir do Microsoft JDBC Driver versão 2.0, o driver também fornece o pacote com.microsoft.sqlserver.jdbc.internals, que inclui o suporte de log para as categorias de log internas a seguir.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|AuthenticationJNI|Registra mensagens em log sobre problemas de autenticação integrada no Windows (quando a propriedade de conexão **authenticationScheme** está definida de maneira implícita ou explícita como **NativeAuthentication**).<br /><br /> Os aplicativos podem definir o nível de log como FINEST e FINE.|  
|SQLServerConnection|Registra em log mensagens na classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Os aplicativos podem definir o nível de log como FINE e FINER.|  
|SQLServerDataSource|Registra mensagens em log nas classes [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) e [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md).<br /><br /> Os aplicativos podem definir o nível de log como FINER.|  
|InputStream|Registra mensagens relativas aos seguintes tipos de dados: java.io.InputStream, java.io.Reader e os tipos de dados que têm um especificador max como tipos de dados varchar, nvarchar e varbinary.<br /><br /> Os aplicativos podem definir o nível de log como FINER.|  
|SQLServerException|Registra mensagens em log na classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerResultSet|Registra em log mensagens na classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Os aplicativos podem definir o nível de log como FINE, FINER e FINEST.|  
|SQLServerStatement|Registra em log mensagens na classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Os aplicativos podem definir o nível de log como FINE, FINER e FINEST.|  
|XA|Registra mensagens para todas as transações XA na classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md). Os aplicativos podem definir o nível de log como FINE e FINER.|  
|KerbAuthentication|Registra mensagens em log sobre a autenticação Kerberos tipo 4 (quando a propriedade de conexão **authenticationScheme** está definida como **JavaKerberos**). O aplicativo pode definir o nível de log como FINE ou FINER.|  
|TDS.DATA|Registra mensagens que contêm a conversa no nível do protocolo TDS entre o driver e o SQL Server. O conteúdo detalhado de cada pacote TDS enviado e recebido é registrado em ASCII e hexadecimal. As credenciais de logon (nomes de usuários e senhas) não são registradas. Todos os outros dados são registrados.<br /><br /> Esta categoria cria mensagens muito detalhadas e detalhadas, e só poderá ser habilitada definindo o nível de registro como FINEST.|  
|TDS.Channel|Esta categoria rastreia ações do canal de comunicação TCP com SQL Server. As mensagens registradas incluem abertura e fechamento de soquete, além de leituras e gravações. Elas também rastreiam mensagens relacionadas a estabelecer uma conexão de Protocolo SSL (SSL) com SQL Server.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINE, FINER ou FINEST.|  
|TDS.Writer|Esta categoria rastreia gravações no canal de TDS. Observe que somente o comprimento das gravações é rastreado, não o conteúdo. Esta categoria também rastreia problemas quando um sinal de atenção é enviado ao servidor para cancelar a execução de uma instrução.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINEST.|  
|TDS.Reader|Esta categoria rastreia determinadas operações de leitura do canal de TDS no nível FINEST. No nível FINEST, o rastreamento pode ser detalhado. Nos níveis WARNING e SEVERE, esta categoria rastreia quando o driver recebe um protocolo TDS inválido do SQL Server antes de o driver fechar a conexão.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINER e FINEST.|  
|TDS.Command|Esta categoria rastreia transições de estado de baixo nível e outras informações associadas à execução de comandos TDS, como execuções de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], buscas do cursor ResultSet, confirmações e assim por diante.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINEST.|  
|TDS.TOKEN|Esta categoria registra somente os tokens dentro dos pacotes TDS e é menos detalhada que a categoria TDS.DATA. Ela só poderá ser habilitada definindo o nível de log como FINEST.<br /><br /> No nível FINEST, esta categoria rastreia tokens de TDS à medida que eles são processados na resposta. No nível SEVERE, esta categoria rastreia quando um token de TDS inválido é encontrado.|  
|SQLServerDatabaseMetaData|Registra mensagens em log na classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerResultSetMetaData|Registra mensagens em log na classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerParameterMetaData|Registra mensagens em log na classe [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerBlob|Registra mensagens em log na classe [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerClob|Registra mensagens em log na classe [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerSQLXML|Registra mensagens em log na classe SQLServerSQLXML interna. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerDriver|Registra em log mensagens na classe [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md). Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerNClob|Registra mensagens em log na classe [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md). Os aplicativos podem definir o nível de log como FINE.|  
  
## <a name="enabling-tracing-programmatically"></a>Habilitando o rastreamento programaticamente  
 O rastreamento pode ser habilitado programaticamente criando um objeto Logger e indicando a categoria a ser registrada. Por exemplo, o código a seguir mostra como habilitar log para instruções SQL:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 Para desabilitar log no seu código, use o seguinte:  
  
```java
logger.setLevel(Level.OFF);  
```  
  
 Para registrar todas as categorias disponíveis, use o seguinte:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 Para desabilitar uma categoria específica de ser registrada, use o seguinte:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Habilitando rastreamento usando o arquivo logging.properties  
 Você também pode habilitar rastreamento usando o arquivo `logging.properties`, que está localizado no diretório `lib` da instalação do JRE (Java Runtime Environment). Este arquivo poderá ser usado para definir os valores padrão para agentes e manipuladores que serão usados quando o rastreamento for habilitado.  
  
 A seguir está um exemplo das configurações que você pode fazer nos arquivos `logging.properties`:  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  Você pode definir as propriedades no arquivo `logging.properties` usando o objeto LogManager que faz parte de java.util.logging.  
  
## <a name="see-also"></a>Confira também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
