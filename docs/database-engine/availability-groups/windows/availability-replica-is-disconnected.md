---
title: A réplica de disponibilidade está desconectada em um grupo de disponibilidade
description: Identifique as possíveis causas de uma réplica estar desconectada em um Grupo de Disponibilidade AlwaysOn.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: troubleshooting
f1_keywords:
- sql13.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
author: cawrites
ms.author: chadam
ms.openlocfilehash: 14050bd328086daabb6fe0ca1c6b570e800f929e
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643140"
---
# <a name="availability-replica-is-disconnected-within-an-always-on-availability-group"></a>A réplica de disponibilidade está desconectada em um Grupo de Disponibilidade AlwaysOn
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da Conexão da Réplica de Disponibilidade|  
|**Problema**|A réplica de disponibilidade está desconectada.|  
|**Categoria**|**Crítico**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>DESCRIÇÃO  
 Esta política verifica o estado da conexão entre as réplicas de disponibilidade. O estado da política é não íntegro quando o estado de conexão da réplica de disponibilidade é DISCONNECTED. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [A réplica de disponibilidade está desconectada](https://go.microsoft.com/fwlink/p/?LinkId=220857) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 A réplica secundária não está conectada à réplica primária. O estado de conexão é DISCONNECTED. Esse problema pode ter sido causado pelo seguinte:  
  
-   A porta de conexão pode estar em conflito com outro aplicativo.  
  
-   O tipo de criptografia ou algoritmo é incompatível.  
  
-   O ponto de extremidade de conexão foi excluído ou não foi iniciado.  
  
-   O transporte está desconectado.  
  
## <a name="possible-solutions"></a>Soluções possíveis  
 Estas são as possíveis soluções para este problema:  
  
-   Verifique a configuração de ponto de extremidade de espelhamento de banco de dados para as instâncias da réplica primária e secundária e atualize a configuração incompatível.  
  
-   Verifique se a porta está em conflito, e se estiver, altere o número da porta.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
