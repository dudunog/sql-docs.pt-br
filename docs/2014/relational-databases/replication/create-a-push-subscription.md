---
title: Criar uma assinatura push | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b571bec94c873b830654126e39d75d554599e5fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721728"
---
# <a name="create-a-push-subscription"></a>Criar uma assinatura push
  Este tópico descreve como criar uma assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou RMO (Replication Management Objects). Para obter informações sobre como criar uma assinatura push para um[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante não, consulte [criar uma assinatura para um assinante não SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie uma assinatura push no Publicador ou Assinante, usando o Assistente para Novas Assinaturas. Siga as páginas no assistente para:  
  
-   Especificar o Publicador e a publicação.  
  
-   Selecione onde os agentes de replicação executarão. Para uma assinatura push, selecione **Executar todos os agentes no Distribuidor (assinaturas push)** na página **Local do Distribution Agent** ou na página **Local do Merge Agent** , dependendo do tipo de publicação.  
  
-   Especifique Assinantes e bancos de dados de assinatura.  
  
-   Especifique os logons e senhas usadas para conexões feitas por agentes de replicação:  
  
    -   Para assinaturas para instantâneos e publicações transacionais, especifique as credenciais na página **Segurança do Distribution Agent** .  
  
    -   Para assinaturas para publicações de mesclagem, especifique as credenciais na página **Segurança do Merge Agent** .  
  
     Para obter informações sobre as permissões exigidas por cada agente, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Especifique uma agenda de sincronização e quando o Assinante deve ser inicializado.  
  
-   Especifique opções adicionais para publicações de mesclagem: tipo de assinatura e valores para filtragem com parâmetros.  
  
-   Especifique opções adicionais para publicações transacionais que permitem assinaturas de atualização: se os Assinantes devem confirmar alterações no Publicador imediatamente ou gravá-las em uma fila; credenciais usadas do Assinante para o Publicador.  
  
-   Opcionalmente, faça o script da assinatura.  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>Para criar uma assinatura push do Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação na qual você deseja criar uma ou mais assinaturas e clique em **Novas Assinaturas**.  
  
4.  Complete as páginas no Assistente para Novas Assinaturas.  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>Para criar uma assinatura push do Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** .  
  
3.  Clique com o botão direito do mouse na pasta **Assinaturas Locais** e depois clique em **Novas Assinaturas**.  
  
4.  Na página **Publicação** do Assistente para Nova Assinatura, selecione **\<Encontrar publicador do SQL Server>** ou **\<Encontrar publicador do Oracle>** na lista suspensa **Publicador**.  
  
5.  Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .  
  
6.  Selecione uma publicação na página **Publicação** .  
  
7.  Complete as páginas no Assistente para Novas Assinaturas.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas push podem ser criadas de forma programada, usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
> [!IMPORTANT]  
>  Quando possível, solicite aos usuários que insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para criar uma assinatura push em um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, verifique se a publicação oferece suporte às assinaturas push, executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql).  
  
    -   Se o valor de **allow_push** for **1**, as assinaturas push terão suporte.  
  
    -   Se o valor de **allow_push** for **0**, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando **allow_push** para **@property** e `true` para **@value**.  
  
2.  No Publicador do banco de dados da publicação, execute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique **@publication**, **@subscriber** e **@destination_db**. Especifique um valor **push** para **@subscription_type**. Para obter informações sobre como atualizar assinaturas, consulte [criar uma assinatura atualizável para uma publicação transacional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique o seguinte:  
  
    -   Os **@subscriber**parâmetros **@subscriber_db**, e **@publication** .  
  
    -   As [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenciais do Windows sob as quais o agente de distribuição no distribuidor é **@job_login** executado **@job_password**para e.  
  
        > [!NOTE]  
        >  As conexões feitas usando a autenticação integrada do Windows sempre usam as credenciais **@job_login** do **@job_password**Windows especificadas por e. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Valor de **0** para **@subscriber_security_mode** e informações de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@subscriber_login** e **@subscriber_password**. Especifique esses parâmetros se for necessário usar a Autenticação do SQL Server para conexão com o Assinante.  
  
    -   Agenda para o trabalho do Distribution Agent para essa assinatura. Para obter mais informações, consulte [especificar agendas de sincronização](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Ao criar uma assinatura push em um Publicador com um Distribuidor remoto, os valores especificados para todos os parâmetros, inclusive *job_login* e *job_password*são enviados para o Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>Para criar uma assinatura push para publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, verifique se a publicação oferece suporte às assinaturas push, executando [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql).  
  
    -   Se o valor de **allow_push** for **1**, a publicação dará suporte às assinaturas push.  
  
    -   Se o valor de **allow_push** não for **1**, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando **allow_push** para **@property** e `true` para **@value**.  
  
2.  No Publicador, no banco de dados de publicação, execute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql), especificando os seguintes parâmetros:  
  
    -   **@publication**. Esse é o nome da publicação.  
  
    -   **@subscriber_type**. Para uma assinatura de cliente, especifique **local** e, para uma assinatura de servidor, especifique **global**.  
  
    -   **@subscription_priority**. Para uma assinatura de servidor, especifique uma prioridade para a assinatura de (**0,00** a **99,99**).  
  
         Para obter mais informações, consulte [detecção e resolução de conflitos de replicação de mesclagem avançada](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  No Publicador, no banco de dados da publicação, execute [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql). Especifique o seguinte:  
  
    -   Os **@subscriber**parâmetros **@subscriber_db**, e **@publication** .  
  
    -   As credenciais do Windows sob as quais o Agente de Mesclagem no distribuidor é **@job_login** executado **@job_password**para e.  
  
        > [!NOTE]  
        >  As conexões feitas usando a autenticação integrada do Windows sempre usam as credenciais **@job_login** do **@job_password**Windows especificadas por e. O Merge Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Valor de **0** para **@subscriber_security_mode** e informações de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@subscriber_login** e **@subscriber_password**. Especifique esses parâmetros se for necessário usar a Autenticação do SQL Server para conexão com o Assinante.  
  
    -   (Opcional) Valor de **0** para **@publisher_security_mode** e informações de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password**. Especifique esses valores se for necessário usar a Autenticação do SQL Server para conexão com o Publicador.  
  
    -   Agenda para o trabalho do Merge Agent para essa assinatura. Para obter mais informações, consulte [especificar agendas de sincronização](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Ao criar uma assinatura push em um Publicador com um Distribuidor remoto, os valores especificados para todos os parâmetros, inclusive *job_login* e *job_password*são enviados para o Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a>Exemplos (Transact-SQL)  
 O exemplo a seguir cria uma nova assinatura push para uma publicação transacional. Os valores de logon e senha são fornecidos em tempo de execução, usando as variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpushsub.sql#sp_addtranpushsubscription_agent)]  
  
 O exemplo a seguir cria uma nova assinatura push para uma publicação de mesclagem. Os valores de logon e senha são fornecidos em tempo de execução, usando as variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepushsub.sql#sp_addmergepushsubscriptionagent)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Crie assinaturas push de forma programada, usando RMO (Replication Management Objects). As classes RMO usadas para criar uma assinatura push dependem do tipo de publicação no qual a assinatura é criada.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você precisar armazenar credenciais, use os [serviços de criptografia](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para criar uma assinatura push em um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar `false`, as propriedades da Etapa 2 estão incorretas ou a publicação não existe no servidor.  
  
4.  Realize uma lógica AND de bit a bit (`&` no Visual C# e `And` no Visual Basic) entre a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> para o resultado de uma lógica bit a bit OR (`|` em Visual C# e `Or` em Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para ativar assinaturas push.  
  
5.  Se não houver banco de dados de assinatura, crie-o usando a classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obter mais informações, consulte [Creating, Altering, and Removing Databases](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md) (Criando, alterando e removendo bancos de dados).  
  
6.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o Publicador criado na Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome do Assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] em que o Distribution Agent é executado no Distribuidor. Essa conta é usada para fazer conexões locais com o Distribuidor e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> quando a assinatura for criada por um membro da função de servidor fixa `sysadmin`; no entanto, é recomendado. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de `true` (padrão) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que seja usado para sincronizar a assinatura. Se você especificar `false`, a assinatura só poderá ser sincronizada programaticamente.  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Assinante.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> .  
  
    > [!IMPORTANT]  
    >  Ao criar uma assinatura push no Publicador com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, são enviados para o Distribuidor como texto sem-formatação. É necessário criptografar a conexão entre o Publicador e o respectivo Distribuidor remoto antes de chamar o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>Para criar uma assinatura push para publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar `false`, as propriedades da Etapa 2 estão incorretas ou a publicação não existe no servidor.  
  
4.  Realize uma lógica AND de bit a bit (`&` no Visual C# e `And` no Visual Basic) entre a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> para o resultado de uma lógica bit a bit OR (`|` em Visual C# e `Or` em Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para ativar assinaturas push.  
  
5.  Se não houver banco de dados de assinatura, crie-o usando a classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obter mais informações, consulte [Creating, Altering, and Removing Databases](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md) (Criando, alterando e removendo bancos de dados).  
  
6.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o Publicador criado na Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome do Assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] na qual o Merge Agent é executado no Distribuidor. Essa conta é usada para fazer conexões locais com o Distribuidor e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> quando a assinatura for criada por um membro da função de servidor fixa `sysadmin`; no entanto, é recomendado. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de `true` (padrão) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que seja usado para sincronizar a assinatura. Se você especificar `false`, a assinatura só poderá ser sincronizada programaticamente.  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Assinante.  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Publicador.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> .  
  
    > [!IMPORTANT]  
    >  Ao criar uma assinatura push no Publicador com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, são enviados para o Distribuidor como texto sem-formatação. É necessário criptografar a conexão entre o Publicador e o respectivo Distribuidor remoto antes de chamar o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo cria uma nova assinatura push para uma publicação transacional. As credenciais da conta do Windows usadas para executar o trabalho do Distribution Agent são passadas em runtime.  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 Esse exemplo cria uma nova assinatura push para uma publicação de mesclagem. As credenciais da conta do Windows usadas para executar o trabalho do Agente de Mesclagem são passadas em runtime.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de assinatura push](view-and-modify-push-subscription-properties.md)   
 [Práticas recomendadas de segurança de replicação](security/replication-security-best-practices.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Conceitos de Replication Management Objects](concepts/replication-management-objects-concepts.md)   
 [Sincronizar uma assinatura push](synchronize-a-push-subscription.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Usar sqlcmd com variáveis de script](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
