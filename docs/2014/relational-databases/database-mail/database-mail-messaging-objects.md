---
title: Objetos do sistema de mensagens do Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3657e45d18ac84ad737a016150692730f736b55f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917698"
---
# <a name="database-mail-messaging-objects"></a>Objetos do sistema de mensagens do Database Mail
  O banco de dados **msdb** é o host de Database Mail. Este banco de dados contém os procedimentos armazenados e objetos de mensagens para o Database Mail. O Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] contém o Assistente para Configuração do Database Mail, que permite habilitar o Database Mail, criar e gerenciar perfis e contas e configurar opções do Database Mail.  
  
##  <a name="objects-in-msdb-database"></a><a name="ComponentsAndConcepts"></a> Objetos no banco de dados **msdb**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser habilitado no banco de dados **msdb** . Porém, o Database Mail não usa o sistema de rede do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Portanto, os usuários não têm que criar um ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para usar o Database Mail. O processo externo do Database Mail usa uma conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] padrão para se comunicar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando habilitado, o Database Mail expõe os seguintes objetos no banco de dados **msdb** .  
  
 Esses objetos são a interface para o Database Mail dentro do banco de dados de host de correio. Outros objetos estão instalados para implementar a funcionalidade oferecida pelos objetos listados acima. No entanto, esses objetos são reservados para uso interno.  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|[sysmail_allitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-allitems-transact-sql)|`View`|Lista todas as mensagens submetidas ao Database Mail.|  
|[sysmail_event_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-event-log-transact-sql)|`View`|Lista mensagens sobre o comportamento do [Database Mail External Program](database-mail-external-program.md).|  
|[sysmail_faileditems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-faileditems-transact-sql)|`View`|Informações sobre mensagens que o Database Mail não conseguiu enviar.|  
|[sysmail_mailattachments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql)|`View`|Informações sobre anexos de mensagens do Database Mail.|  
|[sysmail_sentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-sentitems-transact-sql)|`View`|Informações sobre mensagens que foram enviadas usando o Database Mail.|  
|[sysmail_unsentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql)|`View`|Informações sobre mensagens que o Database Mail está tentando enviar atualmente.|  
|[sp_send_dbmail &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql)|`Stored Procedure`|Envia mensagens de email usando o Database Mail.|  
|[sysmail_delete_log_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql)|`Stored Procedure`|Exclui mensagens do log do Database Mail.|  
|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql)|`Stored Procedure`|Exclui itens de email da fila do Database Mail.|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|`Stored Procedure`|Indica se o Database Mail foi iniciado.|  
|[sysmail_start_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|`Stored Procedure`|Inicia os objetos do Service Broker utilizados pelo programa externo. Esses objetos são iniciados por padrão.|  
|[sysmail_stop_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|`Stored Procedure`|Interrompe os objetos do Service Broker que são utilizados pelo programa externo.|  
  

  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
