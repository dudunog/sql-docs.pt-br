---
title: Trabalhando com notificações de consulta | Microsoft Docs
description: As notificações de consulta permitem solicitar a notificação durante um período de tempo limite quando os dados subjacentes de uma consulta são alterados no SQL Server Native Client.
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 908da6bd9c0b978c273acd7e42cde7c8ad7f954d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84948716"
---
# <a name="working-with-query-notifications"></a>Trabalhando com notificações de consulta
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  As notificações de consulta foram introduzidas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Baseadas na infraestrutura do Service Broker, introduzida no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], as notificações de consulta permitem que os aplicativos sejam notificados em caso de alteração nos dados. Esse recurso é particularmente útil para aplicativos que fornecem um cache de informações de um banco de dados, como um aplicativo da Web, e precisam ser notificados quando os dados de origem são alterados.  
  
 As notificações de consulta permitem que você solicite uma notificação em um tempo limite especificado quando os dados subjacentes de uma consulta são alterados. A solicitação por notificação especifica as opções de notificação, que incluem o nome do serviço, o texto da mensagem e o valor do tempo limite do servidor. As notificações são entregues através de uma fila do Service Broker na qual os aplicativos podem sondar as notificações disponíveis.  
  
 A sintaxe da cadeia de caracteres das opções de notificação de consulta é:  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 Por exemplo:  
  
 `service=mySSBService;local database=mydb`  
  
 As assinaturas de notificação duram mais tempo do que o processo que as inicia, já que um aplicativo pode criar uma assinatura de notificação e, em seguida, ser encerrado. A assinatura permanece válida e a notificação será feita se os dados forem alterados no tempo limite especificado na criação da assinatura. Uma notificação é identificada pela consulta executada, pelas opções de notificação e pelo texto da mensagem, podendo ser cancelada definindo-se o valor de seu tempo limite como zero.  
  
 As notificações só são enviadas uma vez. Para que as notificações de alteração de dados sejam contínuas, é preciso criar uma nova assinatura e executar novamente a consulta depois que cada notificação foi processada.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Os aplicativos cliente nativos normalmente recebem notificações usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando [Receive](../../../t-sql/statements/receive-transact-sql.md) para ler notificações da fila associada ao serviço especificado nas opções de notificação.  
  
> [!NOTE]  
>  Os nomes de tabela devem ser qualificados nas consultas para as quais a notificação é requerida, por exemplo, `dbo.myTable`. Os nomes de tabela devem ser qualificados com nomes de duas partes. A assinatura é considerada inválida se nomes com três ou quatro partes são usados.  
  
 A infraestrutura de notificação baseia-se em um recurso de fila introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Em geral, as notificações geradas no servidor são enviadas através dessas filas para serem processadas posteriormente.  
  
 Para usar notificações de consulta, uma fila e um serviço devem existir no servidor. Eles podem ser criados usando [!INCLUDE[tsql](../../../includes/tsql-md.md)] da seguinte forma:  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  O serviço deve usar o contrato predefinido `https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification` como mostrado acima.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à notificação do consumidor na modificação do conjunto de linhas. O consumidor recebe uma notificação em cada fase da modificação do conjunto de linhas e em qualquer tentativa de alteração.  
  
> [!NOTE]  
>  Passar uma consulta de notificações para o servidor com **ICommand:: execute** é a única maneira válida de assinar notificações de consulta com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo.  
  
### <a name="the-dbpropset_sqlserverrowset-property-set"></a>O conjunto de propriedades DBPROPSET_SQLSERVERROWSET  
 Para dar suporte a notificações de consulta por meio do OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client adiciona as novas propriedades a seguir ao conjunto de propriedades DBPROPSET_SQLSERVERROWSET.  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|O número de segundos que a notificação de consulta permanece ativa.<br /><br /> O padrão é 432000 segundos (5 dias). O valor mínimo é 1 segundo e o valor máximo é 2^31-1 segundos.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|O texto da mensagem da notificação. É definido pelo usuário e não tem um formato predefinido.<br /><br /> Por padrão, a cadeia de caracteres fica vazia. Você pode especificar uma mensagem que contenha entre 1-2000 caracteres.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|As opções de notificação de consulta. Eles são especificados em uma cadeia de caracteres com a sintaxe de valor de *nome* = *value* . O usuário é responsável por criar o serviço e ler as notificações da fila.<br /><br /> O padrão é uma cadeia de caracteres vazia.|  
  
 A assinatura de notificação é sempre confirmada, independentemente do fato de a instrução ter sido executada em uma transação de usuário ou em uma confirmação automática ou se a transação na qual a instrução foi executada tiver sido confirmada ou revertida. A notificação do servidor é acionada mediante uma das seguintes condições inválidas de notificação: alteração dos dados subjacentes ou do esquema ou quando o tempo limite expira; a que ocorrer primeiro. Os registros de notificação são excluídos assim que são disparados. Consequentemente, em caso de recebimento de notificações, o aplicativo deve realizar uma nova assinatura caso queira obter mais atualizações.  
  
 Outra conexão ou thread pode verificar se há notificações na fila de destino. Por exemplo:  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 Observe que SELECT * não exclui a entrada da Fila, ao contrário de RECEIVE \* FROM. Isso irá interromper um thread de servidor se a fila estiver vazia. Se houver entradas na fila durante o momento da chamada, elas serão retornadas imediatamente; caso contrário, a chamada aguardará até que seja feita a entrada na fila.  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 Essa instrução retornará imediatamente um conjunto de resultados vazio se a fila estiver vazia; caso contrário, retornará todas as notificações da fila.  
  
 Se SSPROP_QP_NOTIFICATION_MSGTEXT e SSPROP_QP_NOTIFICATION_OPTIONS forem não nulos e não vazios, o cabeçalho do TDS para notificações de consulta que contém as três propriedades definidas acima é enviado ao servidor em cada execução do comando. Se algum deles for nulo (ou vazio), o cabeçalho não será enviado e DB_E_ERRORSOCCURRED será usado, (ou DB_S_ERRORSOCCURRED se as propriedades estiverem marcadas como opcionais), e o valor do status será definido como DBPROPSTATUS_BADVALUE. A validação é feita em Execute/Prepare. De modo semelhante, DB_S_ERRORSOCCURED será acionado quando as propriedades de notificação da consulta forem definidas para conexões com versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. O valor de status nesse caso é DBPROPSTATUS_NOTSUPPORTED.  
  
 Iniciar uma assinatura não garante que as mensagens subsequentes sejam entregues com êxito. Além disso, nenhuma verificação é feita em relação à validade do nome de serviço especificado.  
  
> [!NOTE]  
>  A preparação de assinaturas nunca fará com que a assinatura seja iniciada; somente a execução da instrução iniciará a assinatura e as notificações de consulta não são impactadas pelo uso dos serviços principais do OLE DB.  
  
 Para obter mais informações sobre o conjunto de propriedades DBPROPSET_SQLSERVERROWSET, consulte [Propriedades e comportamentos](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)do conjunto de linhas.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte a notificações de consulta através da adição de três novos atributos às funções [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) e [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) :  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 Se SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT e SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS não forem NULOS, o cabeçalho do TDS das notificações de consulta que contém os três atributos definidos acima será enviado para o servidor toda vez que o comando for executado. Se um deles for nulo, o cabeçalho não será enviado e SQL_SUCCESS_WITH_INFO será retornado. A validação ocorre na [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360), **SqlExecDirect**e **SqlExecute**, todas que falham se os atributos não forem válidos. De modo semelhante, quando esses atributos de notificação de consulta são definidos para versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ocorre uma falha na execução com SQL_SUCCESS_WITH_INFO.  
  
> [!NOTE]  
>  A preparação de instruções nunca iniciará a assinatura; a assinatura pode ser iniciada com a execução da instrução.  
  
## <a name="special-cases-and-restrictions"></a>Casos especiais e restrições  
 Os seguintes tipos de dados não são suportados para notificações:  
  
-   **text**  
  
-   **ntext**  
  
-   **imagem**  
  
 Se for feita uma solicitação de notificação para um consulta que retorna um desses tipos, a notificação será disparada imediatamente, especificando que não foi possível realizar a assinatura na notificação.  
  
 Se uma solicitação de assinatura for feita para um lote ou procedimento armazenado, outra solicitação de assinatura será feita para cada instrução executada no lote ou procedimento armazenado. As instruções EXECUTE não registrarão notificações, mas enviarão a solicitação de notificação para o comando executado. Se for um lote, o contexto será aplicado às instruções executadas e as mesmas regras descritas anteriormente serão aplicadas.  
  
 Envio de uma consulta para notificação que foi enviada pelo mesmo usuário no mesmo contexto de banco de dados e tem o mesmo modelo, os mesmos valores de parâmetro, a mesma ID de notificação e o mesmo local de entrega de uma assinatura ativa existente, renovará a assinatura existente, redefinindo o novo tempo limite especificado. Isso significa que, se a notificação for solicitada para consultas idênticas, apenas uma notificação será enviada. Isso se aplica a uma consulta duplicada em um lote ou a uma consulta em um procedimento armazenado chamada várias vezes.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
