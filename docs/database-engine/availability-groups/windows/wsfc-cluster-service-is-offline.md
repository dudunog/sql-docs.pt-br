---
title: O serviço de cluster WSFC está offline | Microsoft Docs
description: O estado do cluster WSFC verifica o estado do Cluster de Failover do Windows Server. A política não é íntegra quando o cluster está offline ou no estado de quorum forçado.
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 7231b013f4fabb5e91cf02d6885620cdc876a3a6
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643668"
---
# <a name="wsfc-cluster-service-is-offline"></a>O serviço de cluster WSFC está offline

[!INCLUDE[sql windows only](../../../includes/applies-to-version/sql-windows-only.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado do cluster WSFC|  
|**Problema**|O serviço de cluster WSFC está offline.|  
|**Categoria**|**Crítico**|  
|**Faceta**|Instância do SQL Server|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado do WSFC (Cluster de failover de Windows Server). O estado da política é não íntegro e um alerta é gerado quando o cluster WSFC está offline ou no estado de quorum forçado. Todos os grupos de disponibilidade dentro deste cluster estão offline ou uma ação de recuperação de desastres é necessária.  
  
 O estado da política é íntegro quando o estado do cluster está no quorum normal.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O serviço de cluster WSFC está offline](https://go.microsoft.com/fwlink/p/?LinkId=220849) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 A causa desse problema pode ser um problema de serviço de cluster ou a perda do quorum no cluster.  
  
## <a name="possible-solution"></a>Solução possível  
 Use a ferramenta de Administrador de Cluster para executar o quorum forçado ou o fluxo de trabalho de recuperação de desastres. Se você não conseguir resolver o problema executando o quorum forçado ou a recuperação de desastres, contate o administrador de cluster para ajudar a resolver esse problema. Para obter mais informações, veja [Forçar um cluster WSFC a iniciar sem um quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
