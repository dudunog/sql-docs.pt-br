---
description: Segurança do Agente (Assistente para Nova Publicação)
title: Segurança do agente (Assistente para nova publicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 92534143e42446ef3a1427c6dd6f6f2c110153aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428008"
---
# <a name="agent-security-new-publication-wizard"></a>Segurança do Agente (Assistente para Nova Publicação)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A página **Segurança do Agente** permite especificar as contas nas quais os seguintes agentes executam e fazem conexões com computadores em uma topologia de replicação:  
  
-   O Agente de Instantâneo para todas as publicações.  
  
-   O Agente de Leitor de Log para todas as publicações transacionais.  
  
-   O Agente de Leitor de Fila para publicações transacionais que permitem assinaturas atualizáveis. O trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para esse agente será criado se você especificar **Publicação transacional com assinaturas atualizáveis** na página **Tipo de Publicação**, independentemente do tipo de assinatura atualizável usado. Para obter mais informações sobre assinaturas atualizáveis, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Para obter mais informações sobre permissões requeridas por agentes e práticas recomendadas para segurança de replicação, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opções  
 **Snapshot Agent**  
 Exibido para todas as publicações. Clique em **Configurações de Segurança** para especificar configurações de segurança na caixa de diálogo **Segurança do Agente de Instantâneo** .  
  
 Clique em **Ajuda** na caixa de diálogo **Segurança do Agente de Instantâneo** para obter mais informações sobre as permissões necessárias para contas usadas pelo Agente de Instantâneo.  
  
 **Agente de Leitor de Log**  
 Exibido para todas as publicações transacionais. Clique em **Configurações de Segurança** para especificar configurações de segurança na caixa de diálogo **Segurança do Agente de Leitor de Log** .  
  
 Clique em **Ajuda** na caixa de diálogo **Segurança do Agente de Leitor de Log** para obter mais informações sobre as permissões requeridas para contas usadas pelo Agente de Leitor de Log.  
  
> [!NOTE]  
>  Há um Agente de Leitor de Log para cada banco de dados publicado que usa a replicação transacional. Se uma publicação transacional já existir no banco de dados, as configurações de segurança serão somente leitura. Você pode alterar as configurações na caixa de diálogo **Propriedades de Publicação** , mas as alterações afetam todas as publicações transacionais no banco de dados.  
  
 **Queue Reader Agent**  
 Exibido para todas as publicações transacionais que permitem assinaturas atualizáveis. Clique em **Configurações de Segurança** para especificar configurações de segurança na caixa de diálogo **Segurança do Agente de Leitor de Fila** . O trabalho Agente de Leitor de Fila é criado quando o assistente é concluído; ele não depende da criação de nenhuma assinatura de atualização enfileirada. Se você não planeja criar assinaturas de atualização enfileirada, pode desabilitar o trabalho. Clique com o botão direito do mouse no trabalho (citado no formato: *[\<Publisher>].\<integer>* .) na pasta **Trabalhos** do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e clique em **Desabilitar**.  
  
 Clique em **Ajuda** na caixa de diálogo **Segurança do Agente de Leitor de Fila** para obter mais informações sobre as permissões requeridas para contas usadas pelo Agente de Leitor de Fila.  
  
> [!NOTE]  
>  Há um Agente de Leitor de Fila para cada banco de dados de distribuição (e todos os Publicadores que ele serve). Se uma publicação transacional que permite assinaturas de atualização enfileiradas já existir em qualquer um dos Publicadores que usam um banco de dados de distribuição específico, as configurações de segurança serão somente leitura. Você pode alterar a conta na qual o Agente de Leitor de Fila executa e faz conexões na caixa de diálogo **Propriedades do Distribuidor** , mas as alterações afetam as publicações em todos os Publicadores que usam o banco de dados de distribuição.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Controle de acesso e identidade para replicação](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
