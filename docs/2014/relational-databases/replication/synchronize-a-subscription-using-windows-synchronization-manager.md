---
title: Sincronizar uma assinatura usando o Gerenciador de sincronização do Windows (Gerenciador de sincronização do Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 04b1c5322408f66ab2a4023e3d215cc7e669eab6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745755"
---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager-windows-synchronization-manager"></a>Sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows (Gerenciador de Sincronização do Windows)
  O Gerenciador de Sincronização[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows só poderá ser usado para sincronizar assinaturas para publicações do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução no mesmo computador que o Gerenciador de Sincronização (ele também pode ser usado para sincronizar arquivos offline e páginas da Web). Para usar o Gerenciador de Sincronização:  
  
1.  Habilite a sincronização de assinatura pull com o Gerenciador de Sincronização do Windows na caixa de diálogo **Propriedades de Assinatura – \<Subscriber>: \<SubscriptionDatabase>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md).  
  
2.  Acesse o Gerenciador de Sincronização através do menu **Iniciar** no Windows.  
  
 O Gerenciador de Sincronização permite usar o Resolvedor Interativo para mesclar assinaturas. Normalmente, os conflitos detectados durante a sincronização são resolvidos automaticamente, mas se a resolução interativa estiver habilitada, os conflitos poderão ser resolvidos pelo usuário durante a sincronização. Se a sincronização a ser executada for a do Gerenciador de Sincronização do Windows (como uma sincronização agendada ou sob demanda no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no Replication Monitor) os conflitos serão resolvidos automaticamente sem a intervenção do usuário, de acordo com o resolvedor especificado para o artigo.  
  
> [!NOTE]  
>  A partir do [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] e [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)], as versões de 64 bits do Gerenciador de Sincronização do Windows não podem detectar assinaturas de 32 bits.  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>Para habilitar a sincronização de assinaturas pull com o Gerenciador de Sincronização do Windows  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades de Assinatura – \<Subscriber>: \<SubscriptionDatabase>**, selecione um valor de **Habilitar** para a opção **Usar Gerenciador de Sincronização do Windows**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>Para sincronizar uma assinatura pull com o Gerenciador de Sincronização  
  
1.  Inicie o Gerenciador de Sincronização usando um dos seguintes métodos:  
  
    -   No Internet Explorer, clique em **Ferramentas**e, então, clique em **Sincronizar**.  
  
    -   Clique em **Iniciar**, aponte para **Programas** ou **Todos os Programas**, aponte para **Acessórios**e, então, clique em **Sincronizar**.  
  
    -   Clique em **Iniciar**e em **executar.** Na caixa de diálogo **executar** , digite `mobsync.exe` no campo **abrir** e, em seguida, clique em **OK**.  
  
2.  Na caixa de diálogo **Itens a Serem Sincronizados** , selecione as assinaturas a serem sincronizadas. As assinaturas são listadas sob as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
3.  Clique em **Sincronizar**.  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>Para reinicializar uma assinatura pull com o Gerenciador de Sincronização  
  
1.  Na caixa de diálogo **Itens a Serem Sincronizados** , selecione uma assinatura e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades de Assinatura do SQL Server** , clique em **Reinicializar Assinatura**.  
  
3.  Clique em **Sim**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Por padrão, na próxima vez que a assinatura é sincronizada, um novo instantâneo é aplicado ao banco de dados de assinatura. Para obter mais informações, consulte [Reinicializar as assinaturas](reinitialize-subscriptions.md).  
  
> [!NOTE]  
>  A replicação de mesclagem permite que qualquer alteração pendente seja carregada no Publicador antes do instantâneo ser aplicado, mas essa opção não está disponível no Gerenciador de Sincronização. Para carregar alterações, sincronize a assinatura antes de reiniciá-la.  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>Para definir propriedades de uma assinatura pull no Gerenciador de Sincronização  
  
1.  Na caixa de diálogo **Itens a Serem Sincronizados** , selecione uma assinatura e clique em **Propriedades**.  
  
2.  Exiba e modifique propriedades nas seguintes guias:  
  
    -   **Identificação**  
  
    -   **Logon do Assinante**, **Logon do Distribuidor**e **Logon do Publicador** (apenas para replicação de mesclagem)  
  
    -   **Informações do Servidor Web** (para assinatura de mesclagem em Assinantes que usam SQL Server 2005 ou posterior)  
  
    -   **Outros**  
  
     É recomendável usar a Autenticação do Windows para todas as conexões. Para obter mais informações sobre as permissões que são exigidas pelo Distribution Agent e pelo Merge Agent, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>Para remover uma assinatura pull do Gerenciador de Sincronização  
  
1.  Na caixa de diálogo **Itens a Serem Sincronizados** , selecione uma assinatura e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades de Assinatura do SQL Server** , clique em **Remover Assinatura**.  
  
3.  Selecione uma opção na caixa de diálogo **Remover Assinatura** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>Para usar o Resolvedor Interativo  
  
1.  Habilite o artigo e assinatura a usarem a resolução interativa. Para obter mais informações, consulte [Especificar a resolução interativa de conflitos para artigos de mesclagem](../../relational-databases/replication/publish/specify-merge-replication-properties.md#interactive-conflict-resolution).
  
2.  Após o início da sincronização da assinatura no Gerenciador de Sincronização, o Resolvedor Interativo será iniciado automaticamente se a resolução interativa de conflitos estiver habilitada e se houver conflitos em um ou mais artigos. O Resolvedor Interativo exibe um conflito de cada vez, com uma sugestão de resolução para cada conflito (com base no resolvedor especificado quando a publicação e a assinatura foram criadas).  
  
3.  Opcionalmente, edite qualquer uma das colunas exibidas no Resolvedor Interativo e clique em um dos seguintes botões para resolver o conflito:  
  
    -   **Aceitar Sugestão**  
  
    -   **Aceitar Publicador**  
  
    -   **Aceitar Assinante**  
  
    -   **Resolver Tudo Automaticamente** (todos os conflitos atuais são resolvidos sem entrada adicional)  
  
     Em seguida, a linha selecionada é aplicada ao Publicador e/ou Assinante. Ela é propagada para outros nós na topologia durante sincronizações subsequentes.  
  
> [!NOTE]  
>  As edições serão aplicadas apenas se fizerem parte da linha escolhida para resolução. Por exemplo, se você fizer edições no **Publicador**e, em seguida, clicar em **Aceitar Assinante**, as edições serão descartadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Resolução interativa de conflitos](merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
