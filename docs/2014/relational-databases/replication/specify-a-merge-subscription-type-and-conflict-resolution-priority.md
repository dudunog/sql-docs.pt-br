---
title: Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a19ae6246fe59308283fbaf2f35e2c49f96b140c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055559"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos (SQL Server Management Studio)
   Especifique um tipo de assinatura de mesclagem e prioridade de resolução de conflitos na página **Tipo da Assinatura** do Assistente para Novas Assinaturas. Para mais informações sobre como usar esse assistente, consulte [Create a Pull Subscription](create-a-pull-subscription.md) e [Create a Push Subscription](create-a-push-subscription.md).  
  
 O tipo de assinatura não pode ser modificado após a criação de uma assinatura, mas a prioridade pode ser modificada para o tipo de assinatura de servidor na caixa de diálogo **Propriedades da assinatura- \<Publisher> \<PublicationDatabase> :** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito  
  
1.  Na página **Tipo da Assinatura** do Assistente para Novas Assinaturas, selecione **Cliente** ou **Servidor** para a opção **Tipo da Assinatura** .  
  
2.  Se você selecionar um tipo de assinatura no **Servidor**, digite também um valor (0.00 até 99.99) para a opção **Prioridade para a Resolução de Conflitos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar a prioridade para a resolução de conflitos  
  
1.  Nas **Propriedades da assinatura- \<Publisher> : \<PublicationDatabase> ** no Publicador, insira um valor (0, 0 a 99,99) para a opção de **prioridade** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflitos de replicação de mesclagem avançada](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
