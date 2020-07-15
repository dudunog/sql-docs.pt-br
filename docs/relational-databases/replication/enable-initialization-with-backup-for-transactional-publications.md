---
title: Habilitar a inicialização com backup (transacional)
description: Saiba como habilitar a inicialização de um backup em uma publicação transacional no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0416bc5ff174520ef5548ec6ad91eea647eafaf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653036"
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>Habilitar a inicialização com um backup para publicações transacionais
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para inicializar uma assinatura de uma publicação transacional a partir de um backup, habilite a publicação para permitir a inicialização a partir de um backup e então especifique informações de backup ao criar a assinatura.  
  
-   Habilite a publicação na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publication>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Especifique informações de backup com o procedimento armazenado [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para mais informações sobre os parâmetros exigidos por **sp_addsubscription**, consulte [Inicializar uma assinatura transacional de um Backup &#40;programação de Transact-SQL de replicação&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar a inicialização com um backup  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publication>** , selecione um valor **Verdadeiro** para a opção **Permitir inicialização dos arquivos de backup**.  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura transacional sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
