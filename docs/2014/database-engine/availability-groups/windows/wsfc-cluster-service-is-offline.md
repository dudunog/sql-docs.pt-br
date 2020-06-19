---
title: O serviço de cluster WSFC está offline | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1394b84cca05ef1e3371f21463d20d802ead9841
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936187"
---
# <a name="wsfc-cluster-service-is-offline"></a>O serviço de cluster WSFC está offline
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado do cluster WSFC|  
|**Problema**|O serviço de cluster WSFC está offline.|  
|**Categoria**|**Crítico**|  
|**Faceta**|Instância do SQL Server|  
  
## <a name="description"></a>DESCRIÇÃO  
 Esta política verifica o estado do WSFC (Cluster de failover de Windows Server). O estado da política é não íntegro e um alerta é gerado quando o cluster WSFC está offline ou no estado de quorum forçado. Todos os grupos de disponibilidade dentro deste cluster estão offline ou uma ação de recuperação de desastres é necessária.  
  
 O estado da política é íntegro quando o estado do cluster está no quorum normal.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O serviço de cluster WSFC está offline](https://go.microsoft.com/fwlink/p/?LinkId=220849) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 A causa desse problema pode ser um problema de serviço de cluster ou a perda do quorum no cluster.  
  
## <a name="possible-solution"></a>Solução possível  
 Use a ferramenta de Administrador de Cluster para executar o quorum forçado ou o fluxo de trabalho de recuperação de desastres. Se você não conseguir resolver o problema executando o quorum forçado ou a recuperação de desastres, contate o administrador de cluster para ajudar a resolver esse problema. Para obter mais informações, veja [Forçar um cluster WSFC a iniciar sem um quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
