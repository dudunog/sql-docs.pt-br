---
description: Registro em log e auditoria do Database Mail
title: Log e auditoria do Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fcb4dbe767c549987c6c54a056d0f33f3708a4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499719"
---
# <a name="database-mail-log-and-audits"></a>Registro em log e auditoria do Database Mail
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A funcionalidade de log do Database Mail é criada para fornecer um modo de isolar e corrigir problemas. O Database Mail armazena as informações de log no banco de dados **msdb** . Informações sobre conteúdo de e-mail do Database Mail, status de emails e qualquer mensagem recebida, tais como erros, são registradas em log pelo Database Mail e podem ser usadas para fins de solução de problemas e auditoria.  
  
## <a name="database-mail-logs"></a>Logs do Database Mail  
 Tabelas no banco de dados **msdb** registram informações do [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md). [Exibições do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) expõe as tabelas para fins de solução de problemas. Erros aparecem na exibição [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) quando o Service Broker não consegue ativar o programa externo, se o programa externo encontra erros de rede ou se o servidor SMTP recusa uma mensagem de email. Na eventualidade de o programa externo não conseguir fazer registros nas tabelas do **msdb** , o programa registrará os erros no log de eventos de aplicativos do Windows.  
  
 Tabelas internas do **msdb** contêm as mensagens de email e anexos enviados por meio do Database Mail, além do status atual de cada mensagem. O Database Mail atualiza essas tabelas assim que cada mensagem é processada.  
  
## <a name="database-mail-auditing-tasks"></a>Tarefas de auditoria do Database Mail  
  
|Examinando e gerenciando logs do Database Mail|Link para o tópico|  
|-|-|  
|Verifique o status de entrega de uma mensagem individual|[Verificar o status de mensagens de email enviadas com o Database Mail](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Limpe mensagens, anexos e entradas de log do Database Mail|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|Arquive mensagens e logs do Database Email|[Criar um trabalho do SQL Server Agent para arquivar mensagens e logs de eventos do Database Mail](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
