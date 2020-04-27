---
title: Visão geral da publicação Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 558ee09eeb4419bc354ff3ade9d6586877246b33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022256"
---
# <a name="oracle-publishing-overview"></a>Oracle Publishing Overview
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] em diante, você pode incluir Publicadores Oracle na topologia de replicação, no Oracle versão 9i em diante. Os servidores de publicação podem ser implantados em todos os sistemas operacionais e de hardware com suporte pelo Oracle. O recurso é criado sob a base bem-estabelecida da replicação de instantâneo e da replicação transacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , fornecendo desempenho e usabilidade similares.  
  
 A publicação Oracle foi preterida. A replicação heterogênea para assinantes que não são do SQL Server foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="snapshot-replication-for-oracle"></a>Replicação de instantâneo para Oracle  
 As publicações de instantâneo Oracle são implementadas de forma similar às publicações de instantâneo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Quando o Agente de Instantâneo é executado para uma publicação Oracle, ele se conecta ao Oracle e processa cada tabela na publicação Ao processar cada tabela, o agente recupera as linhas de tabela e cria scripts de esquemas, os quais são armazenados em seguida no compartilhamento de instantâneo da publicação. Todo conjunto de dados é criado sempre que o Agente de Instantâneo for executado, de modo que os gatilhos de rastreamento de alterações não sejam adicionados a tabelas Oracle como ocorre com a replicação transacional. A replicação de instantâneo fornece uma maneira conveniente para migrar os dados com um impacto mínimo no sistema de publicação.  
  
## <a name="transactional-replication-for-oracle"></a>Replicação transacional para Oracle.  
 As publicações transacionais Oracle são implementadas com o uso da arquitetura de publicação transacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; no entanto, as alterações são rastreadas com o uso de uma combinação de gatilhos de banco de dados, no banco de dados Oracle e no Agente de Leitor de Log. Os assinantes de uma publicação transacional Oracle são inicializados automaticamente com o uso da replicação de instantâneo; as alterações subsequentes são rastreadas e distribuídas aos Assinantes à medida que ocorrem por meio do Agente de Leitor de Log.  
  
 Quando uma publicação Oracle é criada, os gatilhos e as tabelas de rastreamento são criados para cada tabela publicada dentro do banco de dados Oracle. Quando as alterações são feitas nas tabelas publicadas, os gatilhos do banco de dados nas tabelas são acionados e inserem informações nas tabelas de rastreamento de replicação para cada linha modificada. O Agente de Leitor de Log do Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] move em seguida as informações das alterações dos dados, das tabelas de rastreamento para o banco de dados de distribuição no Distribuidor. Para concluir, como em uma replicação transacional padrão o Agente de Distribuição move as alterações do Distribuidor para os Assinantes.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](configure-an-oracle-publisher.md)   
 [Glossário de termos da publicação Oracle](glossary-of-terms-for-oracle-publishing.md)   
 [Replicação de banco de dados heterogêneo](heterogeneous-database-replication.md)  
  
  
