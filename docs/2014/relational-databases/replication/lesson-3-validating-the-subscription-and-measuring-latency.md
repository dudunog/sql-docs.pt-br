---
title: 'Lição 3: Validando a assinatura e medindo a latência | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: rothja
ms.author: jroth
ms.openlocfilehash: eba65b6b19054414a13a46ebd2ccb92a28305dde
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065881"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>Lição 3: Validando a assinatura e medindo a latência
  Nesta lição, você usará tokens de rastreadores para verificar se as alterações estão sendo replicadas para o Assinante e para determinar: a latência, o tempo decorrido entre o momento em que a alteração é feita no Publicador, e o momento em que ela aparece no Assinante. Esta lição exige que você tenha concluído a lição anterior, [Lição 2: Criando uma assinatura na publicação transacional](lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>Para inserir um token de rastreamento e exibir informações sobre o token  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e clique em **Iniciar o Replication Monitor**.  
  
     O Replication Monitor é iniciado.  
  
2.  Expanda um grupo Publicador no painel esquerdo; expanda a instância do Publicador e, depois, clique na publicação **AdvWorksProductTrans** .  
  
3.  Clique na guia **Tokens de Rastreamento** .  
  
4.  Clique em **Inserir Rastreador**.  
  
5.  Exiba o tempo decorrido para o token de rastreamento nas seguintes colunas: **Publicador para Distribuidor**, **Distribuidor para Assinante**, **Latência Total**. Um valor **pendente** indica que o token não atingiu um determinado ponto.  
  
## <a name="next-steps"></a>Próximas etapas  
 Nessa lição, você usou tokens de rastreador com êxito, para validar que as alterações de dados sejam replicadas do Publicador para o Assinante. É igualmente possível inserir, atualizar ou excluir dados da tabela **Product** do Publicador e consultar a tabela **Product** do Assinante para exibir essas alterações após serem replicadas.  
  
 Isso encerra o tutorial Replicando Dados entre Servidores Conectados Continuamente Para obter um tutorial semelhante, que utilize replicação de mesclagem, consulte [Tutorial: Replicating Data with Mobile Clients](tutorial-replicating-data-with-mobile-clients.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Medir a latência e validar as conexões para a replicação transacional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
