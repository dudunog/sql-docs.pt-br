---
title: Monitorar o envio de logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], status
- history tables [SQL Server]
- historical information [SQL Server], log shipping
- log shipping [SQL Server], monitoring
- alerts [SQL Server], log shipping
- status information [SQL Server], log shipping
- monitoring log shipping [SQL Server]
ms.assetid: acf3cd99-55f7-4287-8414-0892f830f423
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d480fe510b6d2e252faefaae13d7dd3776c8ec5d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774880"
---
# <a name="monitor-log-shipping-transact-sql"></a>Monitorar envio de logs (Transact-SQL)
  Depois que você configurar o envio de logs, você poderá monitorar as informações sobre o status de todos os servidores de envio de logs. O histórico e status de operações de envio de logs são sempre salvos localmente pelos trabalhos de envio de log. O histórico e status da operação de backup são armazenados no servidor primário e o histórico e status de operações de cópia e restauração são armazenados no servidor secundário. Se você implementou um servidor monitor remoto, estas informações também serão armazenadas no servidor monitor.  
  
 Você pode configurar alertas que serão acionados se as operações de envio de logs não acontecerem como programado. Os erros são encontrados por um trabalho de alerta que observa o status de operações de backup e restauração. Você pode definir os alertas que notificam um operador quando estes erros forem gerados. Se um servidor monitor estiver configurado, um trabalho de alerta gerado pelos erros de todas as operações da configuração de envio de logs é executado no servidor monitor. Se um servidor monitor não for especificado, um trabalho de alerta é executado na instância primária do servidor que monitora a operação de backup. Se um servidor monitor não for especificado, um trabalho de alerta também será executado em cada instância secundária de servidor para monitorar as operações locais de cópia e restauração.  
  
> [!IMPORTANT]  
>  Para monitorar uma configuração de envio de logs, você deve adicionar o servidor monitor quando habilitar o envio de log. Se você adicionar um servidor monitor posteriormente, você deve remover a configuração de envio de logs e em seguida substituí-la por uma configuração que inclui um servidor monitor. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md). Além disso, depois que o servidor monitor for configurado, ele não pode ser alterado sem remover primeiro o envio de logs.  
  
## <a name="history-tables-containing-monitoring-information"></a>Tabelas de histórico que contêm informações de monitoramento  
 As tabelas que monitoram histórico contêm metadados armazenados no servidor monitor. Também é armazenada localmente uma cópia de informações específicas de um determinado servidor primário ou secundário.  
  
 Você pode fazer consultas nestas tabelas para monitorar o status de uma sessão de envio de logs. Por exemplo, para saber sobre o status de envio de logs, verifique o status e o histórico dos trabalhos de backup, de cópia e restauração. Você pode exibir o histórico de envio de logs específico e detalhes de erros consultando as tabelas de monitoramento a seguir.  
  
|Tabela|DESCRIÇÃO|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Armazena ID de trabalho de alerta.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Armazena detalhes de erros dos trabalhos de envio de logs. Você pode fazer consultas nesta tabela para ver os erros de uma sessão de agente. Como opção, você pode classificar os erros por data e hora em que cada um foi registrado. Cada erro é registrado como uma sequência de exceções e erros múltiplos (sequências) por sessão de agente.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Contém detalhes de histórico para agentes de envio de logs. Você pode fazer consultas nesta tabela para ver os detalhes de histórico de uma sessão de agente.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Armazena um registro de monitor para o banco de dados primário em cada configuração de envio de logs, inclusive informações sobre o último arquivo de backup e último arquivo restaurado que é útil para monitoramento.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Armazena um registro de monitor para cada banco de dados secundário, inclusive informações sobre o último arquivo de backup e último arquivo restaurado que é útil para monitoramento.|  
  
## <a name="stored-procedures-for-monitoring-log-shipping"></a>Procedimentos Armazenados para Monitoramento de Envio de Logs  
 O monitoramento e as informações de histórico são armazenados em tabelas no **msdb**, que pode ser acessado com o uso dos procedimentos armazenados de envio de logs. Execute estes procedimentos armazenados nos servidores indicados na tabela a seguir.  
  
|Procedimento armazenado|DESCRIÇÃO|Execute este procedimento em|  
|----------------------|-----------------|---------------------------|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|Retorna registros de monitor para o banco de dados primário especificado da tabela **log_shipping_monitor_primary** .|Servidor monitor ou servidor primário|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|Retorna registros de monitor para o banco de dados secundário especificado da tabela **log_shipping_monitor_secondary** .|Servidor monitor ou servidor secundário|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|Retorna a ID de trabalho do trabalho de alerta.|Servidor monitor ou servidor primário ou secundário se nenhum monitor estiver definido|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|Recupera configurações do banco de dados primário e exibe os valores das tabelas **log_shipping_primary_databases** e **log_shipping_monitor_primary** .|Servidor primário|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|Recupera nomes de banco de dados secundários para um banco de dados primário.|Servidor primário|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|Recupera configurações de bancos de dados primários e exibe os valores das tabelas **log_shipping_secondary**, **log_shipping_secondary_databases** e **log_shipping_monitor_secondary** .|Servidor secundário|  
|[sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|Esse procedimento armazenado recupera a configurações de um banco de dados primário específico no servidor secundário.|Servidor secundário|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)   
 [Tabelas e procedimentos armazenados de envio de logs](log-shipping-tables-and-stored-procedures.md)  
  
  
