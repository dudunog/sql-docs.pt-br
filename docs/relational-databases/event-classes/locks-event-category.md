---
description: Categoria de eventos Bloqueios
title: Categoria de evento de bloqueios | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Locks event category [SQL Server]
- SQL Server event classes, Locks event category
- event classes [SQL Server], Locks event category
- lock escalation [SQL Server], locks event category
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 24bcedd0eb22430bde706ca6565bf7521d3691e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448614"
---
# <a name="locks-event-category"></a>Categoria de eventos Bloqueios
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use as classes de evento na categoria de evento **Bloqueios** para monitorar a atividade de bloqueio em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Essas classes de evento podem ajudar a descobrir problemas de bloqueio causados por vários usuários lendo e modificando dados simultaneamente.  
  
 Como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] frequentemente processa muitos bloqueios, captar as classes de evento **Locks** durante um rastreamento pode incorrer em sobrecarga significativa e resultar em arquivos ou tabelas de rastreamento maiores.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Deadlock Graph](../../relational-databases/event-classes/deadlock-graph-event-class.md)|Fornece uma descrição XML de um deadlock.|  
|[Classe de evento Lock:Acquired](../../relational-databases/event-classes/lock-acquired-event-class.md)|Indica que um bloqueio foi adquirido em um recurso, como uma linha em uma tabela.|  
|[Classe de evento Lock:Cancel](../../relational-databases/event-classes/lock-cancel-event-class.md)|Rastreia solicitações de bloqueios canceladas antes que o bloqueio fosse adquirido (por exemplo, para impedir um deadlock).|  
|[Classe de evento Lock:Deadlock Chain](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|Monitora quando ocorrem condições de deadlock e quais objetos são envolvidos.|  
|[Classe de evento Lock:Deadlock](../../relational-databases/event-classes/lock-deadlock-event-class.md)|Rastreia quando uma transação solicitou um bloqueio em um recurso já bloqueado por outra transação, resultando em um deadlock.|  
|[Classe de evento Lock:Escalation](../../relational-databases/event-classes/lock-escalation-event-class.md)|Indica se um bloqueio mais refinado foi convertido em um bloqueio mais rústico.|  
|[Classe de evento Lock:Released](../../relational-databases/event-classes/lock-released-event-class.md)|Rastreia quando um bloqueio é liberado.|  
|[Classe de evento Lock:Timeout &#40;timeout &#62; 0&#41;](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|Rastreia quando solicitações de bloqueio não podem ser concluídas porque outra transação tem um bloqueio no recurso solicitado. Esse evento só acontece em situações em que o valor de tempo limite de bloqueio é maior que zero.|  
|[Classe de evento Lock:Timeout](../../relational-databases/event-classes/lock-timeout-event-class.md)|Rastreia quando solicitações de bloqueio não podem ser concluídas porque outra transação tem um bloqueio no recurso solicitado.|  
  
  
