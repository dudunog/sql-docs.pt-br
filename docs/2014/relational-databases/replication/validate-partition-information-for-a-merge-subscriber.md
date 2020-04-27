---
title: Validar informações de partição para um assinante de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bada5fc49dc344510164260330699b60a3288cc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63255307"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>Validar informações de partição para um assinante de mesclagem
  Quando você define um filtro de linha com parâmetros para uma publicação de mesclagem, usa uma função que faz referência à informação do Assinante, como o nome de logon do Assinante. Por padrão, a replicação valida a informação do Assinante baseada nessa função, antes de cada sincronização e sempre que um instantâneo é aplicado ao Assinante. O processo de validação assegura que os dados são particionados corretamente para cada Assinante. O comportamento da validação é controlado pela propriedade de publicação **validate_subscriber_info**, que pode ser alterada usando [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) ou na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação**. Para obter mais informações sobre como alterar propriedades de publicação, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
## <a name="how-partition-validation-works"></a>Como a validação de partição funciona  
 Quando uma publicação é filtrada, por exemplo, usando a função **SUSER_SNAME()**, o Agente de Mesclagem aplica o instantâneo inicial a cada Assinante baseado nos dados válidos para a expressão **SUSER_SNAME()** .  
  
 Se a validação é ativada, quando o Assinante se conecta novamente ao Publicador para a sincronização seguinte, o Agente de Mesclagem valida a informação do Assinante e assegura que cada partição de assinante seja a mesma que a recebida no instantâneo inicial. Para cada mesclagem subsequente ou aplicativo de instantâneo, o Agente de Mesclagem valida a partição de cada Assinante.  
  
 Se o Agente de Mesclagem detecta que a função usada na expressão de filtragem retornou um valor diferente daquele do instantâneo inicial, o aplicativo de mesclagem ou de instantâneo falhará, e essa assinatura do Assinante poderá necessitar reinicialização. A reinicialização poderá ser necessária para evitar problemas, que podem surgir se as configurações de mesclagem de um Assinante são alteradas, mas poderá ser suficiente para alterar informações no Assinante, como o nome de logon, novamente ao valor usado no momento do instantâneo original.  
  
 Quando o Agente de Mesclagem valida uma partição, além de validar a partição comparando aos valores retornados por todas as funções usadas em expressões de filtragem, o agente também verifica se o instantâneo foi gerado antes das mudanças que o invalidem, como operações de limpeza de metadados ou mudanças de esquema. Se um instantâneo é muito antigo, o Agente de Mesclagem retornará um erro e você precisará gerar novamente um instantâneo particionado para esse Assinante, baseado em um instantâneo regular atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas frequentes sobre administração de replicação](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Práticas recomendadas para a administração de replicação](administration/best-practices-for-replication-administration.md)   
 [Reinicializar assinaturas](reinitialize-subscriptions.md)   
 [Validar os dados replicados](validate-data-at-the-subscriber.md)  
  
  
