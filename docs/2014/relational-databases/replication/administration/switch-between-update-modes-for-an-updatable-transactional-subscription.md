---
title: Alternar entre modos de atualização para uma assinatura transacional atualizável | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c31814d1e2ab6fac64ffcde883f3cac2439828a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055724"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Alternar entre modos de atualização para uma assinatura transacional atualizável
  Este tópico descreve como alternar entre modos de atualização para uma assinatura de transação atualizável no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique o modo para assinaturas atualizáveis usando o Assistente para Nova Assinatura. Para obter informações sobre como configurar o modo ao usar esse assistente, consulte [Exibir e modificar propriedades de assinatura pull](../view-and-modify-pull-subscription-properties.md).  
  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   É possível realizar failover da atualização imediata para a atualização em fila a qualquer momento. Entretanto, após fazê-lo, não será possível retornar para atualização imediata até que o Assinante ou o Publicador esteja conectado e o Queue Reader Agent tenha aplicado todas as mensagens pendentes na fila para o Publicador.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Quando uma assinatura de atualização para uma publicação transacional oferecer suporte para failover de um modo de atualização para outro, você poderá alternar programaticamente os modos de atualização para tratar situações em que a conectividade muda por um curto intervalo de tempo. O modo de atualização pode ser definido programaticamente e sob demanda usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!NOTE]  
>  Para alterar o modo de atualização após a criação da assinatura, a propriedade **update_mode** deve ser definida como **failover** (que permite a troca de atualização imediata para atualização na fila) ou **failover na fila** (que permite a troca de atualização na fila para atualização imediata) quando a assinatura é criada. Essas propriedades são definidas automaticamente no Assistente para Nova Assinatura.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Para definir o modo de atualização para uma assinatura push  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito na assinatura para a qual se quer definir o modo de atualização e, então, clique em **Configurar Método de Atualização**.  
  
4.  Na caixa de diálogo **definir método de atualização- \<Subscriber> : \<SubscriptionDatabase> ** , selecione **atualização imediata** ou **atualização em fila**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Para definir o modo de atualização para uma assinatura pull  
  
1.  Na caixa de diálogo **Propriedades da assinatura- \<Publisher> : \<PublicationDatabase> ** , selecione um valor de **replicar imediatamente as alterações** ou **filas de alterações** para a opção do método de atualização do **assinante** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para obter mais informações sobre como acessar a caixa de diálogo **Propriedades da assinatura- \<Publisher> \<PublicationDatabase> :** , consulte [Exibir e modificar propriedades da assinatura pull](../view-and-modify-pull-subscription-properties.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Para alternar entre modos de atualização  
  
1.  Verifique se a assinatura oferece suporte para failover executando [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql) para uma assinatura pull ou [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) para uma assinatura push. Se o valor do **modo de atualização** no conjunto de resultados for **3** ou **4**, há suporte para failover.  
  
2.  No Assinante, no banco de dados da assinatura, execute [sp_setreplfailovermode](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql). Especifique **@publisher** , **@publisher_db** , **@publication** e um dos seguintes valores para **@failover_mode** :  
  
    -   **em fila** - failover para atualização em fila quando a conectividade for perdida temporariamente.  
  
    -   **imediato** - failover para a atualização imediata quando conectividade for restaurada.  
  
## <a name="see-also"></a>Consulte Também  
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
