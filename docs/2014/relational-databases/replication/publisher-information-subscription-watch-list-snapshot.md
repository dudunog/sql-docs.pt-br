---
title: Informações do Publicador, lista de inspeção da assinatura (publicação de instantâneo, SQL Server 2005 e posterior) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b84f87aff9684cc08fc0d91fc5de364f816125a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63262153"
---
# <a name="publisher-information-subscription-watch-list-snapshot-publication-sql-server-2005-and-later"></a>Informações do Publicador, Lista de Observação da Assinatura (publicação de instantâneo, SQL Server 2005 e versões posteriores)
   A guia **Lista de Observação da Assinatura** está disponível para os Distribuidores que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores; seu propósito é exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado. Você pode filtrar a lista de assinaturas para ver erros, avisos e qualquer assinatura de desempenho insatisfatório. Essa guia fornece um único local para o administrador monitorar todas as atividades de replicação em um Publicador: o Replication Monitor exibe todas as assinaturas que exigem atenção, com base no tipo de replicação selecionado e na opção escolhida na caixa de listagem suspensa **Mostrar** . Como os itens mostrados nessa guia são baseados no status atual e no desempenho, as assinaturas serão exibidas nessa página somente se corresponderem à opção da caixa de listagem **Mostrar** naquele momento.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a uma assinatura, clique com o botão direito do mouse na linha dessa assinatura e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Mostrar Assinaturas de Instantâneo**  
 Selecione o tipo de assinatura (transacional, instantâneo ou mesclagem) a ser exibida para o Publicador selecionado.  
  
 **Mostrar**  
 Selecione os estados de assinatura a serem exibidos para o tipo de assinatura selecionado. Por exemplo, você pode optar por exibir somente as assinaturas que tiverem um erro.  
  
 **Status**  
 O status de cada assinatura, que é determinado pelo status do Snapshot Agent ou do Distribution Agent (o status com prioridade mais alta é exibido).  
  
 Por padrão, a grade que contém informações de assinatura é classificada pela coluna **Status** . A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Expirando em breve/Expirado  
  
-   Assinatura não inicializada  
  
-   Tentando novamente comando com falha  
  
-   Sincronizando  
  
-   Não sincronizando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **Expirando em breve/Expirado** e **Assinatura não inicializada** são avisos. Quando um aviso é exibido, a coluna **Status** também exibe se um agente está em execução. Por exemplo, o status pode ser **Executando, Expirando em breve/Expirado**.  
  
 O valor de status **Expirando em breve/Expirado** só será exibido se for definido um limite. Para obter informações sobre como definir limites, consulte [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) (Definir limites e avisos no Replication Monitor).  
  
 **Assinatura**  
 O nome de cada assinatura no formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Publicação**  
 O nome da publicação com a qual uma assinatura é sincronizada, no formato: *PublicationDatabaseName: PublicationName*.  
  
 **Última Sincronização**  
 A hora da última execução do Distribution Agent. Se a sincronização estiver em andamento, **Em andamento** será exibido.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a replicação](monitoring-replication.md)  
  
  
