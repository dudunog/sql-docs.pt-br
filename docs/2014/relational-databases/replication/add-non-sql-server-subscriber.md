---
title: Adicionar assinante não SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e36d048b11fcc71b27ab0ab2ee815b0284187c4d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068828"
---
# <a name="add-non-sql-server-subscriber"></a>Adicionar Assinante não SQL Server
  A replicação oferece suporte à criação de assinaturas push para publicações de instantâneo e transacionais para Assinantes Oracle e IBM DB2.  
  
## <a name="options"></a>Opções  
 **Tipo de Assinante a adicionar**  
 Selecione um Assinante Oracle ou um Assinante IBM DB2. Para obter mais informações sobre o suporte para esses Assinantes, consulte [Assinantes não SQL Server](non-sql/non-sql-server-subscribers.md).  
  
 **Nome da fonte de dados**  
 O nome usado para localizar o banco de dados em uma rede. A replicação produz uma sequência de conexão para o banco de dados usando o nome da fonte de dados, combinando com o logon, senha e qualquer opção de conexão especificada na página **Segurança do Agente de Distribuição** neste assistente.  
  
> [!NOTE]  
>  O nome da fonte de dados e a cadeia de conexão não são validados pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até que o Agente de Distribuição tente inicializar a assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura para um assinante não SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
