---
title: Classe de evento SQL:StmtCompleted | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL:StmtCompleted event class
ms.assetid: a55f005d-e020-423c-8940-c24ea1b20104
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85bd8f79f7be5a46e8f714f69a0b61de560a0aed
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051689"
---
# <a name="sqlstmtcompleted-event-class"></a>Classe de evento SQL:StmtCompleted
  A classe de evento SQL:StmtCompleted indica que uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] foi concluída.  
  
## <a name="sqlstmtcompleted-event-class-data-columns"></a>Colunas de dados da classe de evento SQL:StmtCompleted  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|CPU|`int`|Tempo da CPU (em milissegundos) usado pelo evento.|18|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duration|`bigint`|Período de tempo (em microssegundos) utilizado pelo evento.|13|Sim|  
|EndTime|`datetime`|Horário em que o evento foi encerrado.|15|Sim|  
|EventClass|`int`|Tipo de evento = 41.|27|Não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData|`int`|Número de linhas retornadas pela instrução.|25|Sim|  
|IntegerData2|`int`|Deslocamento final (em bytes) da instrução que está sendo executada.|55|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LineNumber|`int`|Número da linha da instrução que está sendo executada.|5|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NestLevel|`int`|O nível de aninhamento do procedimento armazenado se a instrução tiver sido executada em um procedimento armazenado.|29|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|Deslocamento|`int`|O deslocamento inicial da instrução no lote ou procedimento armazenado.|61|Sim|  
|Leituras|`bigint`|Número de leituras de página emitidas pela instrução SQL.|16|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|RowCounts|`bigint`|Número de linhas afetadas por um evento.|48|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Texto da instrução que foi executada.|1|Sim|  
|TransactionID|`bigint`|ID da transação se a instrução foi executada em uma transação.|4|Sim|  
|Gravações|`bigint`|Número de gravações de páginas emitidas pela instrução SQL.|17|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
