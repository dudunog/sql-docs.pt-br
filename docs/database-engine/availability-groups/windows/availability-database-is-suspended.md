---
title: O banco de dados de disponibilidade está suspenso para um grupo de disponibilidade
description: Identifique as causas possíveis para que um banco de dados em um grupo de disponibilidade Always On esteja suspenso.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: end-user-help
f1_keywords:
- sql13.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: cawrites
ms.author: chadam
ms.openlocfilehash: 5843b82c3be84acf24e04ab9dac4b616bed857a6
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641216"
---
# <a name="availability-database-is-suspended-for-an-availability-group"></a>O banco de dados de disponibilidade está suspenso para um grupo de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Suspensão do Banco de Dados de Disponibilidade|  
|**Problema**|O banco de dados de disponibilidade está suspenso.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>DESCRIÇÃO  
 Esta política verifica o estado de movimento de dados do banco de dados secundário (também conhecido como "réplica de banco de dados secundário"). A política ficará em estado não íntegro quando a movimentação de dados for suspensa. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O banco de dados de disponibilidade está suspenso](https://go.microsoft.com/fwlink/p/?LinkId=220860) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 A sincronização de dados nesse banco de dados de disponibilidade pode ter sido suspensa pelo seguinte:  
  
-   Devido a um erro, o sistema pode ter suspendido a sincronização de dados.  
  
-   O administrador de banco de dados pode ter suspendido a sincronização de dados para fins de manutenção.  
  
## <a name="possible-solution"></a>Solução possível  
 Retome a sincronização de dados. Se o problema persistir, verifique o grupo de disponibilidade no log de eventos e diagnostique por que o sistema suspendeu a movimentação de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
