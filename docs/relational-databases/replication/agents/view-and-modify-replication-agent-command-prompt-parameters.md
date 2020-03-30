---
title: Exibir e modificar parâmetros do prompt de comando do Agent
description: Saiba como ver e modificar os parâmetros do prompt de comando usados pelos diferentes agentes de replicação no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6c72c58b0a23f8215d303addfbb2ec9fb65c4489
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321626"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>Exibir e modificar parâmetros do prompt de comando de agentes de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Agentes de replicação são executáveis que aceitam parâmetros de linha de comando. Por padrão, os agentes são executados nas etapas de trabalho do Agent [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, portanto, esses parâmetros podem ser exibidos e modificados usando a caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** . Essa caixa de diálogo está disponível na pasta **Trabalhos** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e na guia **Agentes** no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
> [!NOTE]  
>  As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente.  
  
 Embora seja possível modificar os parâmetros diretamente, em geral, eles são modificados através de um perfil de agente. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Ao acessar os trabalhos de agentes na pasta **Trabalhos** use a tabela a seguir, para determinar o nome do trabalho do agente e os parâmetros disponíveis para cada agente.  
  
|Agente|Nome do trabalho|Para uma lista de parâmetros, consulte...|  
|-----------|--------------|------------------------------------|  
|Snapshot Agent|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Snapshot Agent para uma partição de publicação de mesclagem|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de Leitor de Log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[Agente do Leitor de Log de Replicação](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Merge Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Merge Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Distribution Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Distribution Agent para assinaturas pull|**\<Publicador>-\<PublicationDatabase>-\<Publicação>-\<Assinante>-\<SubscriptionDatabase>-\<GUID>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Queue Reader Agent|**[\<Distributor>].\<integer>**|[Agente de Leitor de Fila de Replicação](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Em assinaturas push para publicações Oracle, é **\<Publisher>-\<Publisher**> em vez de **\<Publisher>-\<PublicationDatabase>**  
  
 \*\*Para assinaturas pull para publicações Oracle, é **\<Publisher>-\<DistributionDatabase**> em vez de **\<Publisher>-\<PublicationDatabase>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Para exibir e modificar os parâmetros da linha de comando dos agentes de replicação do Management Studio  
  
1.  Conecte-se ao computador adequado em [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], e expanda o servidor.  
  
    -   Para assinatura pull no Agente de Distribuição e no Agente de Mesclagem, conecte-se com o Assinante.  
  
    -   Para todos os demais agentes, conecte-se com o Distribuidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse em um trabalho e clique em **Propriedades**.  
  
4.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
5.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Para exibir e modificar os parâmetros da linha de comando do Agente de Distribuição e do Agente de Mesclagem do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Exibir Detalhes**.  
  
4.  Na janela **Assinatura <SubscriptionName>** , clique em **Ação** e depois em **Propriedades do Trabalho de \<AgentName>** .  
  
5.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
6.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
7.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Para exibir e modificar parâmetros de linha de comando do Replication Monitor do Agente de Instantâneo, do Agente de Leitor de Log e do Agente de Leitor de Fila.  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique com o botão direito do mouse em um agente na grade e em **Propriedades**.  
  
4.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
5.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Conceitos dos executáveis do Agente de Replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Visão geral dos agentes de replicação](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
