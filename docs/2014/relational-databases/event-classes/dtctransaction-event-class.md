---
title: Classe de evento DTCTransaction| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- DTCTransaction event class
ms.assetid: 9a2d358e-5b8f-4d0b-8b93-6705c009ad57
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1c72b8c718237582f5a40c56e40e2a51e79e177e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029907"
---
# <a name="dtctransaction-event-class"></a>classe de evento DTCTransaction
  Use a classe de evento **DTCTransaction** para monitorar o estado de transações do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] coordenado pelo MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Isso inclui transações que envolvem dois ou mais bancos de dados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]ou transações distribuídas que envolvem duas ou mais instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="dtctransaction-event-class-data-columns"></a>Colunas de dados da classe de evento DTCTransaction  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BinaryData**|`image`|Representação binária da ID da UOW (Unidade de Trabalho) que identifica exclusivamente essa transação dentro do DTC.|2|Sim|  
|**ClientProcessID**|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventClass**|`int`|Tipo de evento = 19.|27|Não|  
|**EventSequence**|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|`int`|Tipo de subclasse de evento.<br /><br /> 0=Obter endereço<br /><br /> 1=Propagar transação<br /><br /> 3=Fechar conexão<br /><br /> 6=Criar uma nova transação DTC<br /><br /> 7=Inscrição em uma transação DTC<br /><br /> 9=Confirmação interna<br /><br /> 10=Anulação interna<br /><br /> 14= Transação sendo preparada<br /><br /> 15=Transação preparada<br /><br /> 16=Transação sendo anulada<br /><br /> 17=Transação sendo confirmada<br /><br /> 22=Falha da TM no estado preparado<br /><br /> 23=Desconhecido|21|Sim|  
|**GroupID**|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|`int`|Nível de isolamento da transação:|25|Sim|  
|**IsSystem**|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|`nvarchar`|Nome do logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\nomedeusuário).|11|Sim|  
|**LoginSid**|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|**RequestID**|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, se você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Login1 e executar uma instrução como Login2, **SessionLoginName** mostrará Login1 e **LoginName** mostrará Login2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|`datetime`|Horário de início do evento, quando disponível.|14|Sim|  
|**TextData**|`ntext`|Representação textual da UOW (Unidade de Trabalho) que identifica exclusivamente essa transação dentro do DTC.|1|Sim|  
|**TransactionID**|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|`bigint`|Token usado para descrever a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
