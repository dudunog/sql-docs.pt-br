---
title: Monitor de Atividade | Microsoft Docs
description: Saiba como usar o Monitor de Atividade para exibir informações sobre os processos do SQL Server e como esses processos afetam a instância atual do SQL Server.
ms.custom: ''
ms.date: 04/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 747cad801170aa9ef2e4907e96dde1b20ddc268e
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506035"
---
# <a name="activity-monitor"></a>Monitor de Atividade
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O Monitor de Atividade exibe informações sobre os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como esses processos afetam a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
O Monitor de Atividade é uma janela do documento com guias com os seguintes painéis expansíveis e recolhíveis: **Visão geral**, **Processos**, **Esperas Recentes**, **E/S do Arquivo de Dados**, **Consultas Caras Recentes** e **Consultas Caras Ativas**. Quando qualquer painel é expandido, o Monitor de Atividade consulta a instância para obter informações. Quando um painel é recolhido, todas as atividades de consulta são interrompidas para esse painel. Você pode expandir um ou mais painéis ao mesmo tempo para exibir diferentes tipos de atividades na instância.  
 
## <a name="customize-columns"></a>Personalizar colunas 
Nas colunas incluídas nos painéis **Processos**, **Esperas Recentes**, **E/S de Arquivo de Dados**, **Consultas Caras Recentes** e **Consultas Caras Ativas**, é possível personalizar a exibição das seguintes maneiras:  
  
1.  Para reorganizar a ordem das colunas, clique no título de coluna e arraste-o para outro local na faixa de opções de título.  
  
2.  Para classificar uma coluna, clique no nome da coluna.  
  
3.  Para filtrar uma ou mais colunas, clique na seta suspensa no título da coluna e selecione um valor.  

## <a name="more-information"></a>Mais informações  
   
|Descrição|Tópico|  
|-|-|  
|Descreve como abrir o Monitor de Atividade e como definir o intervalo de atualização do Monitor de Atividade.|[Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|Vincula-se a tópicos sobre monitoramento de atividade e desempenho do servidor.|[Monitoramento de desempenho e atividade de servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|  
  
  
