---
title: Algumas réplicas síncronas não são sincronizadas
description: Descreve algumas causas e soluções possíveis para quando uma réplica síncrona não está sincronizada com um grupo de disponibilidade Always On.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
author: cawrites
ms.author: chadam
ms.openlocfilehash: a8e5fc7b3aa708acc3542082ece0d980c938eb34
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583827"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Algumas réplicas síncronas não são sincronizadas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de sincronização de dados de réplicas síncronas|  
|**Problema**|Algumas réplicas síncronas não são sincronizadas.|  
|**Categoria**|**Aviso**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Essa política acumula o estado de sincronização de dados de todas as réplicas de disponibilidade e verifica se há réplicas de disponibilidade que não estão no estado de sincronização esperado. A política está em um estado não íntegro quando o estado de qualquer réplica assíncrona não é SYNCHRONIZING e o estado de qualquer réplica síncrona não é SYNCHRONIZED. Caso contrário, o estado da política é íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas síncronas não estão sincronizadas](https://go.microsoft.com/fwlink/p/?LinkId=220853) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Neste grupo de disponibilidade, pelo menos uma réplica síncrona não está sincronizada no momento. O estado de sincronização da réplica pode ser SYNCHRONIZING ou NOT SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade com o estado de sincronização incorreto e, depois, resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
