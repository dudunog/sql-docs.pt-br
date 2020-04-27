---
title: Algumas réplicas de disponibilidade não estão sincronizando dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fb7d422687d0bc956937b30bae261b28edb3931
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62788249"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>Algumas réplicas de disponibilidade não estão sincronizando dados
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização de Dados de Réplicas de Disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade não estão sincronizando dados.|  
|**Categoria**|**Alerta**|  
|**Particular**|grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Essa política acumula o estado de sincronização de dados de todas as réplicas de disponibilidade no grupo de disponibilidade e verifica se a sincronização de alguma réplica de disponibilidade não está funcionando. A política ficará em estado não íntegro se algum estado de sincronização de dados da réplica de disponibilidade for NOT SYNCRONIZING.  
  
 Essa política ficará em estado íntegro se nenhum estado de sincronização de dados da réplica de disponibilidade for NOT SYNCHRONIZING.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade não estão sincronizando os dados](https://go.microsoft.com/fwlink/p/?LinkId=220852) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Nesse grupo de disponibilidade, pelo menos uma réplica secundária tem um estado de sincronização NOT SYNCHRONIZING e não está recebendo dados da réplica primária.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade em estado NOT SYNCHROINIZING e depois resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
