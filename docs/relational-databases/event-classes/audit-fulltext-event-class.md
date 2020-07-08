---
title: Classe de evento Audit Fulltext | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 95e4c5fd-e16f-446e-b42b-105495a8f39a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8bab0dc383ba6d427656cddf14b0ab253d6b313
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85630027"
---
# <a name="audit-fulltext-event-class"></a>Classe de evento Audit Fulltext
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento **Audit Fulltext** ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta e se comunica com o processo de daemon de filtro de texto completo.  
  
## <a name="audit-fulltext-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Fulltext  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**Erro**|**int**|O número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se esse evento informar um erro.|31|Sim|  
|**EventSequence**|**int**|A sequência de determinado evento dentro da solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de conexão usado pelo logon. 1 = Não em pool, 2 = Em pool.|21|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|1 = êxito. 0 = falha. Por exemplo, o valor 1 indica êxito em uma verificação de permissões e o valor 0 indica falha nessa verificação.|23|Sim|  
|**TargetLoginName**|**int**|Para ações direcionadas a um logon (por exemplo, adição de um novo logon), o nome do logon de destino.|42|Sim|  
|**TargetLoginSid**|**int**|Para ações direcionadas a um logon (por exemplo, adição de um novo logon), o SID (número de ID de segurança) do logon de destino.|43|Sim|  
|**TextData**|**ntext**|Informações sobre o evento de texto completo. Normalmente este campo fornece informações sobre a conexão entre o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o processo de daemon de filtro de texto completo|1|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
