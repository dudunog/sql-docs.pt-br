---
title: Classe de evento FT:Crawl Aborted | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Crawl Aborted event class
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 843e15f6f4cc0e683bb24a9a4709d66707111737
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052962"
---
# <a name="ftcrawl-aborted-event-class"></a>Classe de evento FT:Crawl Aborted
  A classe de evento **FT:Crawl Aborted** indica que uma exceção foi encontrada durante um rastreamento de texto completo. O erro normalmente provoca a interrupção do rastreamento de texto completo. Verifique o log de eventos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ou o log do rastreamento para obter informações mais detalhadas sobre o erro.  
  
## <a name="ftcrawl-aborted-event-class-data-columns"></a>Colunas de dados da classe de evento FT:Crawl Aborted  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID do banco de dados no qual o rastreamento de texto completo está sendo executado. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**Erro**|**int**|Número de erro de um determinado evento. Frequentemente, esse é o número do erro armazenado na tabela **sysmessages** .|31|Sim|  
|**EventClass**|**int**|Tipo de evento = 157.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**ObjectID**|**int**|ID do objeto, atribuída pelo sistema, no qual o rastreamento de texto completo era executado quando ocorreu a falha.|22|Sim|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**State**|**int**|Equivalente a um código de estado de erro.|30|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
