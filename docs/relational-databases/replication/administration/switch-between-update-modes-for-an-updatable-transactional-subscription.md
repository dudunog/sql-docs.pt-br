---
title: Alternar entre modos (transacional atualizável)
description: Descreve como alternar entre modos de atualização em uma publicação transacional atualizável com o SSMS (SQL Server Management Studio) ou o T-SQL (Transact-SQL).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 8f9480787ced42ad66602bb34db98d1c2d53bd35
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321973"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Alternar entre modos de atualização para uma assinatura transacional atualizável
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como alternar entre modos de atualização para uma assinatura de transação atualizável no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique o modo para assinaturas atualizáveis usando o Assistente para Nova Assinatura. Para obter informações sobre como configurar o modo ao usar esse assistente, consulte [Exibir e modificar propriedades de assinatura pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para alternar entre modos de atualização para uma assinatura transacional atualizável usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   É possível realizar failover da atualização imediata para a atualização em fila a qualquer momento. Entretanto, após fazê-lo, não será possível retornar para atualização imediata até que o Assinante ou o Publicador esteja conectado e o Queue Reader Agent tenha aplicado todas as mensagens pendentes na fila para o Publicador.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Quando uma assinatura de atualização para uma publicação transacional oferecer suporte para failover de um modo de atualização para outro, você poderá alternar programaticamente os modos de atualização para tratar situações em que a conectividade muda por um curto intervalo de tempo. O modo de atualização pode ser definido programaticamente e sob demanda usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!NOTE]  
>  Para alterar o modo de atualização após a criação da assinatura, a propriedade **update_mode** deve ser definida como **failover** (que permite a troca de atualização imediata para atualização na fila) ou **failover na fila** (que permite a troca de atualização na fila para atualização imediata) quando a assinatura é criada. Essas propriedades são definidas automaticamente no Assistente para Nova Assinatura.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Para definir o modo de atualização para uma assinatura push  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito na assinatura para a qual se quer definir o modo de atualização e, então, clique em **Configurar Método de Atualização**.  
  
4.  Na caixa de diálogo **Configurar Método de Atualização – \<Subscriber>: \<SubscriptionDatabase>** , selecione **Atualização imediata** ou **Atualização na fila**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Para definir o modo de atualização para uma assinatura pull  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Publisher>: \<PublicationDatabase>** , selecione um valor de **Replicar as atualizações imediatamente** ou **Enfileirar alterações** para a opção **Método de atualização do assinante**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para obter mais informações sobre como acessar a caixa de diálogo **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** , consulte [Exibir e modificar propriedades de assinatura pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Para alternar entre modos de atualização  
  
1.  Verifique se a assinatura oferece suporte para failover executando [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) para uma assinatura pull ou [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) para uma assinatura push. Se o valor do **modo de atualização** no conjunto de resultados for **3** ou **4**, há suporte para failover.  
  
2.  No Assinante, no banco de dados da assinatura, execute [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Especifique `@publisher`, `@publisher_db`, `@publication`e um dos valores a seguir para `@failover_mode`:  
  
    -   **em fila** - failover para atualização em fila quando a conectividade for perdida temporariamente.  
  
    -   **imediato** - failover para a atualização imediata quando conectividade for restaurada.  
  
## <a name="see-also"></a>Consulte Também  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
