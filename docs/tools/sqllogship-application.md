---
title: Aplicativo sqllogship
description: O aplicativo sqllogship realiza uma operação de backup, cópia ou restauração e as tarefas de limpeza associadas para uma configuração de envio de logs em um banco de dados SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: af98af52bfe6416c489be821fa2d8b27092fac27
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918347"
---
# <a name="sqllogship-application"></a>Aplicativo sqllogship
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  O aplicativo **sqllogship** realiza uma operação de backup, cópia ou restauração e as tarefas de limpeza associadas de uma configuração de envio de logs. A operação é realizada em uma instância específica do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para um banco de dados específico.  
  
 ![Ícone do Link do tópico](../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter as convenções de sintaxe, confira [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ -verboselevel level ] [ -logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-server** _instance_name_  
 Especifica a instância da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde a operação será executada. A instância do servidor a especificar depende da operação de envio de logs que está sendo especificada. Para **-backup**, *instance_name* deve ser o nome do servidor primário em uma configuração de envio de logs. Para **-copy** ou **-restore**, *instance_name* deve ser o nome de um servidor secundário em uma configuração de envio de logs.  
  
 **-backup** _primary_id_  
 Realiza uma operação de backup do banco de dados primário cuja ID primária é especificada por *primary_id*. É possível obter esta ID selecionando-a na tabela do sistema [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) ou usando o procedimento armazenado [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md) .  
  
 A operação de backup cria o backup de log no diretório de backup. O aplicativo **sqllogship** limpa os arquivos de backup antigos, com base no período de retenção dos arquivos. Em seguida, o aplicativo registra o histórico da operação de backup no servidor primário e o servidor monitor. Por fim, o aplicativo executa [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md), que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **-copy** _secondary_id_  
 Executa uma operação para copiar os backups de um servidor secundário especificado do banco de dados secundário, ou bancos de dados, cuja ID secundária é especificada por *secondary_id*. É possível obter esta ID selecionando-a na tabela do sistema [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) ou usando o procedimento armazenado [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) .  
  
 A operação copia os arquivos de backup do diretório de backup para o diretório de destino. O aplicativo **sqllogship** registra o histórico da operação de cópia no servidor secundário e no servidor do monitor.  
  
 **-restore** _secondary_id_  
 Realiza uma operação de restauração no servidor secundário especificado do banco de dados, ou bancos de dados secundários, cuja ID secundária é especificada por *secondary_id*. É possível obter esta ID usando o procedimento armazenado **sp_help_log_shipping_secondary_database** .  
  
 Qualquer arquivo de backup no diretório de destino criado após o ponto de restauração mais recente é restaurado no banco de dados ou bancos de dados secundários. O aplicativo **sqllogship** limpa os arquivos de backup antigos, com base no período de retenção dos arquivos. Em seguida, o aplicativo registra o histórico da operação de backup no servidor primário e o servidor monitor. Por fim, o aplicativo executa **sp_cleanup_log_shipping_history**, que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **-verboselevel** _level_  
 Especifica o nível das mensagens adicionadas ao histórico do envio de logs. *level* é um dos seguintes inteiros:  
  
|Nível|Descrição|  
|-----------|-----------------|  
|0|Não emite nenhuma mensagem de rastreamento ou de depuração.|  
|1|Emite mensagens para tratamento de erros.|  
|2|Emite mensagens para tratamento de erros e avisos.|  
|**3**|Emite mensagens informativas, avisos e mensagens de tratamento de erros. Esse é o valor padrão.|  
|4|Emite todas as mensagens de depuração e de rastreamento.|  
  
 **-logintimeout** _timeout_value_  
 Especifica o tempo designado para tentar efetuar o login à instância do servidor antes da tentativa expirar. O padrão é 15 segundos. *timeout_value* é **int** _._  
  
 **-querytimeout** _timeout_value_  
 Especifica o tempo designado para iniciar a operação especificada antes da tentativa expirar. O padrão é sem período de expiração. *timeout_value* é **int** _._  
  
## <a name="remarks"></a>Comentários  
 Recomendamos a utilização das opções de backup, copiar e restaurar para realizar as tarefas de backup, copiar e restaurar quando for possível. Para iniciar esses trabalhos em uma operação em lote ou em outro aplicativo, chame o procedimento armazenado [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) .  
  
 O histórico do envio de logs criado por **sqllogship** é intercalado com o histórico criado pelos trabalhos de backup, cópia e restauração do envio de logs. Se você pretende usar **sqllogship** repetidamente para realizar as operações de backup, cópia ou restauração de uma configuração de envio de logs, considere desabilitar o(s) trabalho(s) de envio de logs correspondente(s). Para obter mais informações, consulte [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md).  
  
 O aplicativo **sqllogship** , SqlLogShip.exe, é instalado no diretório x:\Arquivos de Programas\Microsoft SQL Server\130\Tools\Binn.  
  
## <a name="permissions"></a>Permissões  
 **sqllogship** usa a Autenticação do Windows. A conta Autenticação do Windows onde o comando é executado requer acesso ao diretório e às permissões [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do Windows O requisito depende de qual opção é especificada pelo comando **sqllogship** : **-backup**, **-copy**ou **-restore** .  
  
|Opção|Acesso ao diretório|Permissões|  
|------------|----------------------|-----------------|  
|**-backup**|Requer o acesso leitura/gravação ao diretório de backup.|Requer as mesmas permissões da instrução BACKUP. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md).|  
|**-copy**|Requer o acesso leitura ao diretório de backup e o acesso gravação ao diretório copiar|Exige as mesmas permissões do procedimento armazenado [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) .|  
|**-restore**|Requer o acesso leitura/gravação ao diretório copiar.|Requer as mesmas permissões da instrução RESTORE. Para obter mais informações, veja [RESTORE &#40;Transact-SQL&#41;](../t-sql/statements/restore-statements-transact-sql.md).|  
  
> [!NOTE]  
>  Para encontrar os caminhos dos diretórios de backup e cópia, execute o procedimento armazenado **sp_help_log_shipping_secondary_database** ou exiba a tabela **log_shipping_secondary** no **msdb**. Os caminhos dos diretórios de backup e de destino estão nas colunas **backup_source_directory** e **backup_destination_directory** , respectivamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  
