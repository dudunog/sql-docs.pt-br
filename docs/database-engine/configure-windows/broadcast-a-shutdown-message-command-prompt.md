---
title: Difundir uma mensagem de desligamento (prompt de comando) | Microsoft Docs
description: Descubra como usar o comando net send para difundir uma mensagem no SQL Server. Veja como determinar quais usuários estão atualmente conectados ao SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 85d2bac016287afd060cdf727eeea47a6b78d725
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759211"
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>Difundir uma mensagem de desligamento (prompt de comando)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como difundir uma mensagem de desligamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o comando **net send** . Na mensagem, inclua a hora em que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será interrompida de forma que os usuários possam terminar suas tarefas.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>Para difundir uma mensagem de desligamento  
  
1.  Em um prompt de comando, digite:  
  
     **net send /users "mensagem"**  
  
     A opção **/users** especifica que a mensagem será enviada a todos os usuários conectados no servidor  
  
> [!NOTE]  
>  O comando **net send** exige que o serviço de mensagens seja executado nos computadores de envio e de recebimento. O serviço de mensagens é desabilitado por padrão no Windows Server 2003. Para obter informações sobre o **net send**, consulte a documentação do Windows.  
  
 Em sua rede, pode ser mais apropriado contatar os usuários por e-mail ou telefone. Para determinar quais usuários estão conectados atualmente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o Monitor de Atividade. Para obter informações sobre o Monitor de Atividade, veja [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) e [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
