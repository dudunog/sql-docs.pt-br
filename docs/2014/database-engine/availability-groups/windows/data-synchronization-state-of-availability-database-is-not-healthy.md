---
title: O estado de sincronização de dados do banco de dados de disponibilidade não está íntegro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ed541e86bf531dd9681e9926e4acb6d1bdc6042
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936857"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização dos Dados do Banco de Dados de Disponibilidade|  
|**Problema**|O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro.|  
|**Categoria**|**Aviso**|  
|**Particular**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política acumula o estado de sincronização de dados de todos os bancos de dados de disponibilidade (também chamados de "réplicas de banco de dados") na réplica de disponibilidade. A política estará em estado não íntegro quando alguma réplica de banco de dados não estiver no estado de sincronização de dados esperado. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro](https://go.microsoft.com/fwlink/p/?LinkId=220858) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 O estado de sincronização de dados deste banco de dados de disponibilidade não é íntegro. Em uma réplica de disponibilidade de confirmação de transação, todos os bancos de dados de disponibilidade devem estar no estado SYNCHRONIZING. Em uma réplica de disponibilidade da confirmação síncrona, todo banco de dados de disponibilidade deve estar no estado SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solução possível  
 Use a política de réplica de banco de dados para localizar a réplica de banco de dados em estado de sincronização de dados não íntegro e depois resolva o problema na réplica de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
