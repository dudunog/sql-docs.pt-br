---
title: Classe de evento Mount Tape | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Mount Tape event class
ms.assetid: 4c595e0a-d968-47d3-a84f-9b6857342671
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ebb5aef29f6f3cf56ecdf36fcc4b59b33f113f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756022"
---
# <a name="mount-tape-event-class"></a>classe de evento Mount Tape
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento Mount Tape ocorre quando uma solicitação de montagem de fita é recebida. Use essa classe de evento para monitorar solicitações de montagem de fita e o seu êxito ou falha.  
  
## <a name="mount-tape-event-class-data-columns"></a>Colunas de dados de classe de evento Mount Tape  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE *database* ou o banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma instância especificada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duration|**bigint**|Período de tempo (em microssegundos) utilizado pelo evento.|13|Sim|  
|EndTime|**datetime**|Para eventos de Solicitação de Montagem, o tempo limite da montagem, se houver um tempo-limite; caso contrário, o tempo do evento em si (em tais casos,  StartTime indica o tempo da solicitação de montagem correspondente).|15|Sim|  
|EventClass|**int**|Tipo de evento = 195.|27|Não|  
|EventSequence|**int**|A sequência de um evento especificado na solicitação.|51|Não|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 1 = Solicitação de montagem de fita<br /><br /> 2 = Montagem de fita completa<br /><br /> 3 = Montagem de fita cancelada|21|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMAIN\\*username*).|11|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|ID da sessão em que o evento ocorreu.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|*nome do dispositivo físico* [ ( *nome do dispositivo lógico* ) ]. O nome de dispositivo lógico é exibido somente se definido na exibição de catálogo sys.backup_devices.|1|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
