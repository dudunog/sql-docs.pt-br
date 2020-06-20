---
title: Caixa de diálogo ' configurações do distribuidor ' | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6f6fbc408e9a81506db12670a620693464df6b17
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010757"
---
# <a name="sql-server-replication-distributor-settings-dialog-box"></a>Caixa de diálogo Replicação do SQL Server ' configurações do distribuidor '
  A caixa de diálogo **Configurações do Distribuidor** permite alterar configurações para Distribuidores que foram adicionados ao painel esquerdo no Replication Monitor.  
  
## <a name="options"></a>Opções  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Monitor de Replicação conecte-se ao Distribuidor e recupere informações de status.  
  
 **Conexão**  
 Clique para exibir a caixa de diálogo **Conectar ao Servidor** . Isso permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar ao Distribuidor.  
  
 **Atualizar automaticamente o status deste Distribuidor e de suas publicações**  
 Selecione para permitir que o Monitor de Replicação atualize automaticamente o status para o Distribuidor. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status com base no intervalo de sondagem pela opção **Taxa de atualização** . Para obter mais informações sobre atualização no Replication Monitor, consulte [Caching, Refresh, and Replication Monitor Performance](monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores inferiores resultam em sondagem mais frequente. Isto poderá afetar o desempenho no Distribuidor se você estiver monitorando muitos Publicadores. Recomendamos que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostre para todos os Publicadores deste Distribuidor no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não afetam a maneira como a replicação funciona.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)  
  
  
