---
description: editores não SQL Server
title: Publicadores não SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9560875e4db3a644644238b0140fadb33cf1877d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420440"
---
# <a name="non-sql-server-publishers"></a>editores não SQL Server  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A publicação de dados de origens que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite consolidar dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode assinar um instantâneo ou dados transacionais publicados de um banco de dados Oracle. Para obter mais informações sobre a publicação do Oracle, consulte [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md) (Visão geral de publicação do Oracle).  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte aos seguintes cenários heterogêneos para replicação transacional e de instantâneo:  
  
-   Publicando dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para não assinantes do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

-   A publicação de dados para e do Oracle tem as seguintes restrições:  

  |Replicação |2016 ou anterior |2017 ou posterior |
  |:-----------|:---------------|:-------------|
  |Replicação do Oracle |Dá suporte apenas ao Oracle 10g ou anterior |Dá suporte apenas ao Oracle 10g ou anterior |
  |Replicação para o Oracle |Até Oracle 12c |Sem suporte |
  | &nbsp; | &nbsp; | &nbsp; |


 A replicação heterogênea para assinantes que não são do SQL Server foi preterida. A publicação Oracle foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 A publicação de banco de dados que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é ideal para os seguintes cenários:  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|Implantações de aplicativos do[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desenvolva com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver operando em dados replicados de banco de dados que não são do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores de preparo de data warehouse|Mantenha os bancos de dados de preparo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizado com um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migração para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Teste o seu aplicativo em tempo real com relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver reproduzindo as alterações do sistema de fonte. Alterne para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando estiver satisfeito com a migração.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
