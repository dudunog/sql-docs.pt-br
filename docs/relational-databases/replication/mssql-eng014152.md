---
description: MSSQL_ENG014152
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 0087219c660270afc75623cff7024dda1957b0e1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463207"
---
# <a name="mssql_eng014152"></a>MSSQL_ENG014152
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14152|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: agente %s agendado para tentar novamente. %s|  
  
## <a name="explanation"></a>Explicação  
 O agente de replicação especificado foi programado para repetir a operação solicitada. O processo continua repetindo até alcançar o número máximo configurado de tentativas de repetição para a etapa de trabalho.  
  
 Normalmente, uma repetição ocorre devido a um dos seguintes motivos:  
  
-   O valor **QueryTimeout** é excedido.  
  
-   O valor **LoginTimeout** é excedido.  
  
-   O processo de replicação foi escolhido como uma vítima de deadlock.  
  
## <a name="user-action"></a>Ação do usuário  
 Se a mensagem de repetição não for frequente, nenhuma ação é exigida do usuário.  
  
 Use [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md) para exibir a definição atual do número máximo de vezes que a etapa **Executar agente** do agente de replicação especificado será repetida. É possível usar o parâmetro `@retry_attempts` do procedimento armazenado [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) para ajustar o número de vezes que uma etapa de trabalho é repetida.  
  
 Se a mensagem de repetição ocorrer com frequência, você deverá solucionar o problema com base na mensagem que está causando a repetição. Verifique o histórico do agente para mensagens que indicam por que a nova tentativa teve que ser programada. Em alguns casos, talvez seja necessário habilitar o log mais detalhado do agente de replicação. Para obter mais informações sobre como configurar o log para replicação, consulte o artigo [312292](https://support.microsoft.com/kb/312292)na Base de Dados de Conhecimento Microsoft.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
