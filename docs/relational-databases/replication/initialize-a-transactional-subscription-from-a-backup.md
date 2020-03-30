---
title: Inicializar a assinatura do backup (transacional)
description: Saiba como usar procedimentos armazenados de replicação para inicializar uma publicação Transacional de um backup em SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7d2da79cc46ac546099e492af3b6d5f4f726a2a2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75320473"
---
# <a name="initialize-a-transactional-subscription-from-a-backup"></a>Inicializar uma assinatura transacional de um backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Embora uma assinatura a uma publicação transacional seja geralmente inicializada com um instantâneo, é possível inicializar uma assinatura de backup usando procedimentos de replicação armazenados. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Para inicializar um assinante transacional a partir de backup  
  
1.  Para uma publicação existente, certifique-se de que a publicação dê suporte à capacidade de inicializar do backup, executando [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) no Publicador no banco de dados de publicação. Observe o valor de **allow_initialize_from_backup** no conjunto de resultados.  
  
    -   Se o valor for **1**, a publicação oferece suporte a essa funcionalidade.  
  
    -   Se o valor for **0**, execute [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor igual a **allow_initialize_from_backup** para `@property` e um valor igual a **true** para `@value`.  
  
2.  Para uma nova publicação, execute [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor de **true** para **allow_initialize_from_backup**. Para obter mais informações, consulte [Criar uma assinatura](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder dados do assinante, ao usar **sp_addpublication** ou **sp_changepublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
3.  Crie um backup do banco de dados de publicação usando a instrução [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
4.  Restaure o backup no Assinante usando a instrução [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
5.  No Publicador no banco de dados de publicação, execute o procedimento armazenado [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique os seguintes parâmetros:  
  
    -   `@sync_type` – valor igual a **inicializar com backup**.  
  
    -   `@backupdevicetype` – o tipo de dispositivo de backup: **lógico** (padrão), **disco** ou **fita**.  
  
    -   `@backupdevicename` – o dispositivo de backup lógico ou físico a ser usado para a restauração.  
  
         Para um dispositivo lógico, especifique o nome do dispositivo de backup especificado quando **sp_addumpdevice** foi usado para criar o dispositivo.  
  
         Para um dispositivo físico, especifique um caminho completo e nome de arquivo, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` ou `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional) `@password` – uma senha fornecida durante a criação do conjunto de backup.  
  
    -   (Opcional) `@mediapassword` – uma senha fornecida durante a formatação do conjunto de mídias.  
  
    -   (Opcional) `@fileidhint` – identificador do conjunto de backup a ser restaurado. Por exemplo, especificar **1** indica o primeiro conjunto de backup na mídia de backup e **2** indica o segundo conjunto de backup.  
  
    -   (Opcional para dispositivos de fita) `@unload` – especifique um valor igual a **1** (padrão) se a fita deve ser descarregada da unidade após a conclusão da restauração e **0** se ela não deve ser descarregada.  
  
6.  (Opcional) Para uma assinatura pull, execute [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) e [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) no Assinante no banco de dados de assinatura. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Opcional) Iniciar o Distribution Agent. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) ou [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
