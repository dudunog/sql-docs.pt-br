---
title: Caixa de diálogo Replicação do SQL Server ' informações do distribuidor ' | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.Distributor.Publications.f1
- sql12.rep.monitor.Distributor.commonjobs..f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2d738066e4832c029743d53f7ec99dbb1b6fe5cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721365"
---
# <a name="distributor-information-dialog-box"></a>Caixa de diálogo informações do distribuidor 
Este tópico fornece informações sobre a caixa de diálogo **distribuidor** 

## <a name="publications"></a>Publicações

  A guia **Publicações** fornece informações resumidas sobre todas as publicações no Distribuidor selecionado no painel esquerdo.  
  
### <a name="options"></a>Opções  
 As informações que são exibidas sobre as publicações com suporte do Distribuidor incluem uma coluna que contém a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador. Caso contrário, as informações de publicação serão iguais às informações de publicação fornecidas quando você exibe publicações na exibição Publicador do Replication Monitor. Para obter mais informações sobre as colunas da guia **Publicações** , consulte [Publisher Information, Publications](publisher-information-publications.md).  

## <a name="subscription-watch-list"></a>Lista de observação de assinaturas

### <a name="transactional-replication"></a>Replicação transacional 
  As informações de assinaturas transacionais incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação transacional, SQL Server 2005 e posterior&#41;](publisher-information-subscription-watch-list-transactional.md).  

### <a name="merge-replication"></a>Replicação de mesclagem
  As informações de assinaturas de publicação de mesclagem incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação de mesclagem, SQL Server 2005 e posterior&#41;](publisher-information-subscription-watch-list-merge-publication.md). 

### <a name="snapshot-replication"></a>Replicação de instantâneo
  As informações de assinaturas de publicação de instantâneo incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação de instantâneo, SQL Server 2005 e posterior&#41;](publisher-information-subscription-watch-list-snapshot.md).  

## <a name="agents"></a>Agentes
   A guia **Agentes** exibe informações sobre os agentes e trabalhos de manutenção associados com o Publicador e o Assinante.  
  
 Os agentes disponíveis na guia **Agentes** de uma exibição Distribuidor no Distribuidor incluem todos os agentes disponíveis na guia **Agentes** de um Publicador. No entanto, a guia **Agentes** de uma exibição Distribuidor no Distribuidor também inclui um Agente Distribuidor e um Merge Agent.  
  
 Para obter mais informações sobre os agentes Snapshot, Log Reader e Queue Reader, e os trabalhos de manutenção, consulte [Publisher Information, Agents](publisher-information-agents.md). Observe que, quando você exibe informações de agente na guia **Agentes** de um Distribuidor, as informações do Publicador estão presentes para os agentes Snapshot e Log Reader. No entanto, na guia **Agentes** de uma exibição Distribuidor no Distribuidor, ainda é possível selecionar **Agente Distribuidor** e **Merge Agent**.  
  
### <a name="options"></a>Opções  
 As seções a seguir descrevem os dados exibidos nesta guia do Agente Distribuidor e do Merge Agent.  
  
### <a name="distributor-agent"></a>Agente Distribuidor  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro    
-   Repetir    
-   Executando    
-   Não está em execução    
-   Nunca iniciado  
  
 **Editor**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Hora da última inicialização**  
 A última hora de início do agente.  
  
 **Permanência**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual os comandos de inicialização são confirmados no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **Latency**  
 É o tempo, em segundos, que decorreu entre a alteração mais recente sendo confirmada no banco de dados de publicação e o comando correspondente sendo confirmado no banco de dados de distribuição.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmado no banco de dados de distribuição durante a execução mais recente do agente. Um comando é igual a uma alteração de dados, como uma atualização.  
  
 **Avg. #Cmds**  
 O número médio de comandos por transação durante a execução mais recente do agente.  
  
### <a name="merge-agent"></a>Merge Agent  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro    
-   Repetir    
-   Executando    
-   Não está em execução    
-   Nunca iniciado  
  
 **Editor**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Hora da última inicialização**  
 A última hora de início do agente.  
  
 **Permanência**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual as alterações são confirmadas no banco de dados de distribuição.  
  
 **Inserções do Publicador**  
 Número de comandos INSERT aplicados no Publicador.  
  
 **Atualizações do Publicador**  
 Número de comandos UPDATE aplicados no Publicador.  
  
 **Exclusões do Publicador**  
 Número de comandos DELETE aplicados no Publicador.  
  
 **Conflitos do Publicador**  
 O número de conflitos por segundo que ocorrem no Publicador durante o processo de mesclagem.  
  
 **Inserções do Assinante**  
 Número de comandos INSERT aplicados no Assinante.  
  
 **Atualizações do Assinante**  
 Número de comandos UPDATE aplicados no Assinante.  
  
 **Exclusões do Assinante**  
 Número de comandos DELETE aplicados no Assinante.  
  
 **Conflitos do Assinante**  
 O número de conflitos por segundo que ocorrem no Assinante durante o processo de mesclagem.  
  
 
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Monitorando a replicação](monitoring-replication.md)  
  
  
