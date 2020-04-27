---
title: Classe de evento Broker:Conversation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d6f29eba93e7841d2d64db57266d8f2ad859377
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62664362"
---
# <a name="brokerconversation-event-class"></a>Classe de evento Broker:Conversation
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera uma classe de evento **Broker:Conversa** para relatar o progresso de uma conversa do Agente de Serviços.  
  
## <a name="brokerconversation-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Conversation  
  
|Coluna de dados|Type|DESCRIÇÃO|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores transmitidos pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|`int`|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|`int`|A ID do banco de dados que é especificada pela instrução de *banco de dados* USE. A ID do banco de dados padrão, se nenhuma instrução de *banco de dados*USE tiver sido emitida. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor de um banco de dados usando a função **DB_ID** .|3|Sim|  
|**EventClass**|`int`|O tipo de classe de evento capturado. Sempre **124** para **Broker:Conversa**.|27|Não|  
|**EventSequence**|`int`|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|`nvarchar`|O tipo de subclasse de evento. Esse tipo fornece mais informações sobre cada classe de evento.|21|Sim|  
|**GUID**|`uniqueidentifier`|A identificação de conversa do diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|**HostName**|`nvarchar`|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função **HOST_NAME** .|8|Sim|  
|**IsSystem**|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 0 = usuário<br /><br /> 1 = sistema|60|Não|  
|**LoginSid**|`image`|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**MethodName**|`nvarchar`|O grupo de conversa ao qual a conversa pertence.|47|Não|  
|**NTDomainName**|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|`nvarchar`|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|`nvarchar`|O identificador de conversa do diálogo.|34|Não|  
|**Priority**|`int`|O nível de prioridade da conversa.|5|Sim|  
|**RoleName**|`nvarchar`|A função do identificador de conversa. É **initiator** (iniciador) ou **target**(destino).|38|Não|  
|**ServerName**|`nvarchar`|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**Severidade**|`int`|A severidade do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se esse evento informar um erro.|29|Não|  
|**SPID**|`int`|A identificação de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|`datetime`|Horário de início do evento, quando disponível.|14|Sim|  
|**TextData**|`ntext`|O estado atual da conversa. Um dos seguintes:<br /><br /> **Portanto**. Saída iniciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processou um BEGIN CONVERSATION para esta conversa, mas nenhuma mensagem foi enviada.<br /><br /> **Si**. Entrada iniciada. Outra instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] iniciou uma nova conversa com a instância atual, mas a instância atual não terminou de receber a primeira mensagem. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá criar a conversa neste estado se a primeira mensagem estiver fragmentada ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receber mensagens fora de ordem. Entretanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá criar a conversa no estado CO se a primeira transmissão recebida para a conversa contiver a primeira mensagem completa.<br /><br /> **Co**. Conversando. A conversa foi estabelecida, e ambos os lados da conversa podem enviar mensagens. A maioria das comunicações de um serviço típico acontece quando a conversa está nesse estado.<br /><br /> **Di**. Entrada desconectada. O lado remoto da conversa emitiu uma instrução END CONVERSATION. A conversa permanecerá nesse estado até o lado local emitir uma instrução END CONVERSATION. Um aplicativo ainda pode receber mensagens para a conversa. Como o lado remoto da conversa encerrou a conversa, um aplicativo não pode enviar mensagens nesta conversa. Quando um aplicativo emite uma instrução END CONVERSATION, a conversa passa para o estado fechado (CD).<br /><br /> **Fazer**. Saída desconectada. O lado local da conversa emitiu uma instrução END CONVERSATION. A conversa permanecerá neste estado até o lado remoto da conversa reconhecer a instrução END CONVERSATION. Um aplicativo não pode enviar ou receber mensagens para a conversa. Quando o lado remoto da conversa reconhece a instrução END CONVERSATION, a conversa passa para o estado fechado (CD).<br /><br /> **Er**. Erro. Ocorreu um erro neste ponto de extremidade. As colunas de erro, severidade e estado contêm informações sobre o erro específico que ocorreu.<br /><br /> **CD**. Fechado. O ponto de extremidade da conversa não está mais em uso.|1|Sim|  
|**ID da transação**|`bigint`|ID da transação atribuída pelo sistema.|4|Não|  
  
 A tabela a seguir lista os valores de subclasse para essa classe de evento.  
  
|ID|Subclasse|Descrição|  
|--------|--------------|-----------------|  
|1|SEND Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento de **envio** de mensagem [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando o executa uma instrução Send.|  
|2|END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento **END CONVERSATION** quando [!INCLUDE[ssDE](../../includes/ssde-md.md)] o executa uma instrução END CONVERSATION que não inclui a cláusula WITH ERROR.|  
|3|END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento **END CONVERSATION WITH ERROR** quando [!INCLUDE[ssDE](../../includes/ssde-md.md)] o executa uma instrução END CONVERSATION que inclui a cláusula WITH ERROR.|  
|4|Broker Initiated Error|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento de **erro iniciado pelo agente** sempre que [!INCLUDE[ssSB](../../includes/sssb-md.md)] o cria uma mensagem de erro. Por exemplo, quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não pode encaminhar com êxito uma mensagem para um diálogo, o agente cria uma mensagem de erro para o diálogo e gera esse evento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não gera esse evento quando um programa aplicativo encerra uma conversa com um erro.|  
|5|Terminate Dialog|[!INCLUDE[ssSB](../../includes/sssb-md.md)] encerrou o diálogo. [!INCLUDE[ssSB](../../includes/sssb-md.md)] encerra os diálogos em respostas às condições que impedem que eles continuem, mas que não sejam erros ou o encerramento normal de uma conversa. Por exemplo, remover um serviço fará com que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] encerre todos os diálogos daquele serviço.|  
|6|Received Sequenced Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera uma classe de evento **Received Exsequenciated Message** quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o recebe uma mensagem que contém um número de sequência de mensagem. Todos os tipos de mensagens definidos pelo usuário são mensagens sequenciadas. [!INCLUDE[ssSB](../../includes/sssb-md.md)] gera uma mensagem não sequenciada em dois casos:<br /><br /> Mensagens de erro geradas pelo [!INCLUDE[ssSB](../../includes/sssb-md.md)] não são sequenciadas.<br /><br /> Confirmações de mensagens podem não ter sequência. Para eficiência, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inclui a mensagem de qualquer confirmação disponível como parte de uma mensagem sequenciada. Porém, se um aplicativo não enviar uma mensagem sequenciada para o ponto de extremidade remoto em um período específico, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] criará uma mensagem não sequenciada para a confirmação da mensagem.|  
|7|Received END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento Received END CONVERSATION quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebe uma mensagem End Dialog do outro lado da conversa.|  
|8|Received END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento **recebido encerrar conversa com erro** quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o recebe um erro definido pelo usuário do outro lado da conversa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não gera esse evento quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebe um erro definido pelo agente.|  
|9|Received Broker Error Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento de **mensagem de erro do Broker recebido** quando [!INCLUDE[ssSB](../../includes/sssb-md.md)] o recebe uma mensagem de erro definida pelo agente do outro lado da conversa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não gera esse evento quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] recebe uma mensagem de erro gerada por um aplicativo.<br /><br /> Por exemplo, se o banco de dados atual contiver uma rota padrão para um banco de dados de encaminhamento, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] encaminhará uma mensagem com um nome de serviço desconhecido para o banco de dados de encaminhamento. Se esse banco de dados não puder rotear a mensagem, o agente nesse banco de dados criará uma mensagem de erro e retornará essa mensagem de erro para o banco de dados atual. Quando o banco de dados atual recebe o erro gerado pelo agente do banco de dados de encaminhamento, o banco de dados atual gera um evento **Received Broker Error Message** .|  
|10|Received END CONVERSATION Ack|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera uma classe de evento **Received END CONVERSATION ACK** quando o outro lado de uma conversa reconhece uma caixa de diálogo end ou uma mensagem de erro enviada por esse lado da conversa.|  
|11|BEGIN DIALOG|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento **BEGIN DIALOG** quando o mecanismo de banco de dados executa um comando BEGIN DIALOG.|  
|12|Dialog Created|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gera um evento de caixa de [!INCLUDE[ssSB](../../includes/sssb-md.md)] **diálogo criado** quando o cria um ponto de extremidade para uma caixa de diálogo. [!INCLUDE[ssSB](../../includes/sssb-md.md)] cria um ponto de extremidade sempre que um novo diálogo é estabelecido, independentemente de o banco de dados atual ser o iniciador ou o destino do diálogo.|  
|13|END CONVERSATION WITH CLEANUP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento END CONVERSATION WITH CLEANUP quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] executa uma instrução END CONVERSATION que inclui a cláusula WITH CLEANUP.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
