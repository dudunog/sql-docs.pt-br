---
title: Alocando uma alça de declaração | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 85678c5b03a77910c73bd5b8bac8d0e40d52c252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291533"
---
# <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para que um aplicativo possa executar uma instrução, deve alocar um identificador de instrução. Ele faz isso chamando **SQLAllocHandle** com o parâmetro *HandleType* definido para SQL_HANDLE_STMT e *InputHandle* apontando para uma alça de conexão.  
  
 Os atributos da instrução são características do identificador de instrução. O exemplo de atributos de instrução pode incluir o uso de indicadores e o tipo de cursor a ser usado com o conjunto de resultados da instrução. Os atributos de declaração são definidos com [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md), e suas configurações atuais são recuperadas usando [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md). Não há nenhum requisito de que um aplicativo tenha definido qualquer atributo de instrução; todos os atributos de instrução têm padrões e alguns são específicos do driver.  
  
 Tome cuidado ao usar várias opções de conexão e instrução do ODBC. Chamar [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com *fOption* definido para SQL_ATTR_LOGIN_TIMEOUT controla o tempo que um aplicativo espera por uma tentativa de conexão enquanto espera para estabelecer uma conexão (0 especifica uma espera infinita). Os sites que têm tempos de resposta lentos podem definir este valor alto para verificar se as conexões têm tempo suficiente para serem estabelecidas. No entanto, o intervalo deve sempre ser baixo o suficiente para dar ao usuário uma resposta em um tempo razoável se o driver não puder se conectar.  
  
 Chamar **SQLSetStmtAttr** com *fOption* definido para SQL_ATTR_QUERY_TIMEOUT define um intervalo de tempo de consulta para ajudar a proteger o servidor e o usuário de consultas de longa duração.  
  
 Chamar **SQLSetStmtAttr** com *fOption* definido para SQL_ATTR_MAX_LENGTH limita a quantidade de dados de **texto** e **imagem** que uma declaração individual pode recuperar. Chamar **SQLSetStmtAttr** com *fOption* definido para SQL_ATTR_MAX_ROWS também limita um conjunto de linhas para as *primeiras* n linhas, se isso é tudo o que o aplicativo requer. Observe que a configuração SQL_ATTR_MAX_ROWS faz com que o driver emita uma instrução SET ROWCOUNT ao servidor. Isso afeta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas as declarações, incluindo gatilhos e atualizações.  
  
 Tome cuidado quando você for definir estas opções. Será melhor se todos os identificações de instrução em um identificador de conexão tiverem as mesmas configurações para SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS. Se o driver alternar de um identificador de instrução para outro com valores diferentes para essas opções, o driver deverá gerar as instruções SET TEXTSIZE e SET ROWCOUNT adequadas para alterar as configurações. O driver não pode colocar essas instruções no mesmo lote que a instrução SQL do usuário, pois a instrução SQL pode conter uma instrução que deve ser a primeira instrução em um lote. O driver deve enviar as instruções SET TEXTSIZE e SET ROWCOUNT em um lote separado que automaticamente gera uma viagem de ida-e-volta adicional ao servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de consultas &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
