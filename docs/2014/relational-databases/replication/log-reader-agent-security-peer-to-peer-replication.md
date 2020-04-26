---
title: Segurança do Agente de Leitor de Log (replicação ponto a ponto) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6bcf7d78fd550404f81f9cc303414303ad82504
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "63000353"
---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Segurança do Agente de Leitor de Log (replicação ponto a ponto)
   A página **Segurança do Agente de Leitor de Log** permite especificar as contas nas quais o Agente de Leitor de Log executa e efetua conexões em cada par. Para obter informações sobre as permissões necessárias para os agentes e as melhores práticas de segurança da replicação, consulte [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md) e [Melhores práticas de segurança da replicação](security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Há um Agente de Leitor de Log para cada banco de dados publicado que usa a replicação transacional. Se o Agente de Leitor de Log de um banco de dados já foi configurado (para uma publicação em uma execução anterior desse assistente ou para outra publicação transacional no mesmo banco de dados), você não poderá trocar as credenciais que ele usa nesse assistente. Se você especificar credenciais novas, elas serão ignoradas. Para alterar credenciais, use a caixa de diálogo **Propriedades de Publicação** . Para obter mais informações, consulte [Exibir e modificar as configurações de segurança de replicação](security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opções  
 Clique no botão de propriedades (**...**) na linha de cada computador par para acessar a caixa de diálogo **Segurança do Agente de Leitor de Log** . Clique em **Ajuda** na caixa de diálogo **Segurança do Agente de Leitor de Log** iniciada, para obter mais informações sobre as permissões necessárias para as contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas na caixa de diálogo, serão exibidas informações de conexão para o Assinante na grade.  
  
 **Agentes para o Publicador**  
 O nome de cada instância de servidor de computador par.  
  
 **Banco de dados par**  
 O banco de dados que serve como banco de dados de publicação e banco de dados de assinatura em cada nível.  
  
 **Conexão com o Distribuidor**  
 O contexto no qual a conexão com o Distribuidor é feita. A conexão local com o Distribuidor é sempre feita usando o contexto da conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado e, portanto, esse campo sempre exibirá **Representar '\<Domain>\\<Login\>'** ou **Representar '\<Computer>\\<Login\>'**.  
  
 **Conexão com o Publicador**  
 O contexto no qual a conexão com o Publicador é feita. A conexão com o Publicador pode ser feita usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um logon ou usando o contexto da conta do Windows na qual o agente é executado. O campo exibe uma das seguintes opções: **Usar logon '\<Login>'**, **Representar '\<Domain>\\<Login\>'** ou **Representar '\<Computer>\\<Login\>'**. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar uma topologia ponto a ponto &#40;Programação Transact-SQL de replicação&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
