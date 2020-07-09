---
title: Classe de evento OLEDB Errors | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- OLEDB Errors event class
ms.assetid: 0ce1e906-5d92-42f2-ab38-8771ad5ca008
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64df0d85fb8e4bb9e3ea54c7d8613a1a39ac3406
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726236"
---
# <a name="oledb-errors-event-class"></a>classe de evento OLEDB Errors
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento OLEDB Errors ocorre no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando uma chamada para um provedor OLE DB retorna um erro. Inclua esta classe de evento em rastreamentos para exibir uma falha de HRESULT de um provedor OLE DB.  
  
 Quando a classe de evento OLEDB Errors é incluída no rastreamento, a quantidade de sobrecarga criada depende da frequência com que os erros do provedor OLE DB ocorrem em relação ao banco de dados durante o rastreamento. Se tais erros ocorrerem com frequência, o rastreamento poderá impedir desempenho de forma significativa.  
  
## <a name="oledb-errors-event-class-data-columns"></a>Coluna de dados da classe de evento OLEDB Errors  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução de *banco de dados* USE ou o *banco de dados* padrão se nenhuma instrução de banco de dados USE tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Erro|**int**|O HRESULT retornado pelo provedor.|31|Sim|  
|EventClass|**int**|Tipo de evento = 61.|27|Não|  
|EventSequence|**int**|Sequência de classe de evento OLE DB em lote.|51|Não|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LinkedServerName|**nvarchar**|Nome do servidor vinculado.|45|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\Nomedeusuário).|11|Sim|  
|LoginSid|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|MethodName|**nvarchar**|Nome do método OLE DB.|47|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ProviderName|**nvarchar**|Nome do provedor OLE DB.|46|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**nvarchar**|Parâmetros enviados e recebidos na chamada OLE DB.|1|Não|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Objetos Automation no Transact-SQL](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
