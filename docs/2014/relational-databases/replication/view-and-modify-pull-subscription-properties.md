---
title: Exibir e modificar propriedades de assinatura pull | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b847a22d31bbf3ea7540c55339fe27531134125
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063714"
---
# <a name="view-and-modify-pull-subscription-properties"></a>Exibir e modificar propriedades de assinatura pull
  Este tópico descreve como exibir e modificar propriedades de assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para exibir e modificar propriedades de assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exiba as propriedades da assinatura pull do Publicador ou do Assinante na caixa de diálogo **Propriedades da assinatura- \<Publisher> \<PublicationDatabase> :** , que está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Há mais propriedades visíveis no Assinante, e as propriedades podem ser modificadas no Assinante. É igualmente possível exibir propriedades no Publicador, na guia **Todas as Assinaturas** , disponível no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>Para exibir propriedades de assinatura pull no Publicador do Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação apropriada, clique com o botão direito do mouse em uma assinatura e, então, clique em **Propriedades**.  
  
4.  Exiba as propriedades. Em seguida, clique em **OK**.  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>Para exibir e modificar as propriedades de assinatura pull no Assinante do Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>Para exibir propriedades de assinatura pull no Publicador do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Propriedades**.  
  
4.  Exiba as propriedades. Em seguida, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas pull podem ser modificadas e suas propriedades acessadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para visualizar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  No Assinante, execute [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql). Especifique **@publisher** , **@publisher_db** , e **@publication** . Isso retorna informações sobre a assinatura que é armazenada em tabelas do sistema no Assinante.  
  
2.  No Assinante, execute [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql). Especifique **@publisher** , **@publisher_db** , **@publication** e um dos seguintes valores para **@publication_type** :  
  
    -   **0** - Assinatura pertence à uma publicação transacional.  
  
    -   **1** - Assinatura pertence à uma publicação de instantâneo.  
  
3.  No Publicador, execute [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql). Especifique **@publication** e **@subscriber** .  
  
4.  No Publicador, execute [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), especificando **@subscriber**. Isso exibe informações sobre o Assinante.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para alterar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  No Assinante, execute [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql), especificando **@publisher** , **@publisher_db** , **@publication** , um valor de **0** (transacional) ou **1** (instantâneo) para **@publication_type** , a propriedade de assinatura sendo alterada como **@property** e o novo valor como **@value** .  
  
2.  (Opcional) No Assinante, no banco de dados da assinatura, execute [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql). Especifique a ID do trabalho de Agente de Distribuição para **@jobid** e as seguintes propriedades do pacote DTS (Data Transformation Services):  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Isso altera as propriedades de pacote DTS de uma assinatura.  
  
    > [!NOTE]  
    >  O ID de trabalho pode ser obtido executando [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql).  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>Para exibir as propriedades de uma assinatura pull para uma publicação de mesclagem  
  
1.  No Assinante, execute [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql). Especifique **@publisher** , **@publisher_db** , e **@publication** .  
  
2.  No Assinante, execute [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql). Especifique **@publisher** , **@publisher_db** , e **@publication** um valor de 2 para **@publication_type** .  
  
3.  No Publicador, execute [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) para exibir informações de assinatura. Para retornar informações sobre uma assinatura específica, você deve especificar **@publication** , **@subscriber** e um valor de **pull** para **@subscription_type** .  
  
4.  No Publicador, execute [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), especificando **@subscriber**. Isso exibe informações sobre o Assinante.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>Para alterar as propriedades de uma assinatura pull para uma publicação de mesclagem  
  
1.  No Assinante, execute [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql). Especifique **@publication** , **@publisher** , **@publisher_db** , a propriedade de assinatura sendo alterada como **@property** e o novo valor como **@value** .  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO usadas para exibir ou modificar as propriedades da assinatura pull dependem do tipo de publicação em que a assinatura pull está inscrita.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para exibir ou modificar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe no servidor.  
  
6.  (Opcional) Para alterar as propriedades, defina um novo valor para um das propriedades de <xref:Microsoft.SqlServer.Replication.TransPullSubscription> que podem ser definidas e depois chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para exibir as novas configurações, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recarregar as propriedades para o artigo.  
  
8.  Feche todas as conexões.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>Para exibir ou modificar as propriedades de uma assinatura pull de uma publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe no servidor.  
  
6.  (Opcional) Para alterar as propriedades, defina um novo valor para um das propriedades de <xref:Microsoft.SqlServer.Replication.MergePullSubscription> que podem ser definidas e depois chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para exibir as novas configurações, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recarregar as propriedades para o artigo.  
  
8.  Feche todas as conexões.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
