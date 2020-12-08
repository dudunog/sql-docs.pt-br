---
title: SQL Server, objeto Cache de planos | Microsoft Docs
description: Saiba mais sobre o objeto Plan Cache, que fornece contadores para monitorar como o SQL Server usa a memória para armazenar objetos, como gatilhos e procedimentos armazenados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 265b6e877101d69b6af76b1c31ad1aa572989fdd
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505598"
---
# <a name="sql-server-plan-cache-object"></a>SQL Server, objeto Cache de planos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto **Plan Cache** fornece contadores para monitorar como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a memória para armazenar objetos, como procedimentos armazenados e instruções e gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc e preparados. Diversas instâncias do objeto **Plan Cache** podem ser monitoradas ao mesmo tempo, com cada instância representando um tipo de plano diferente para monitorar.  
  
 Esta tabela descreve os contadores **SQLServer:Plan Cache**.  
  
|Contadores SQL Server Plan Cache|Descrição|  
|------------------------------------|-----------------|  
|**Taxa de Acertos do Cache**|Taxa entre acertos e pesquisas do cache.|  
|**Base do Índice de Ocorrência no Cache**|Apenas para uso interno.| 
|**Contagens de Objeto do Cache**|Número de objetos do cache no cache.|  
|**Páginas do Cache**|Número de páginas de 8 quilobytes (KB) usado por objetos do cache.|  
|**Objetos do cache em uso**|Número de objetos do cache em uso.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância do Cache de Plano|Descrição|  
|-------------------------|-----------------|  
|**_Total**|Informações para todos os tipos de instâncias do cache.|  
|**Planos Sql**|Os planos de consulta produzidos de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, inclusive consultas parametrizadas automaticamente ou de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] preparadas usando **sp_prepare** ou **sp_cursorprepare**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenará em cache os planos para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc para reutilização posterior se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] idêntica for executada mais tarde. Consultas parametrizadas pelo usuário (mesmo se não preparadas explicitamente) também são monitoradas como Planos SQL Preparados.|  
|**Planos de Objeto**|Planos de consulta gerados ao criar um procedimento armazenado, função ou gatilho.|  
|**Associar árvores**|Árvores normalizadas para exibições, regras, colunas computadas e restrições de verificação.|  
|**Procedimentos armazenados estendidos**|Informações do catalogo para procedimentos armazenados estendidos.|  
|**Tabelas temporárias & variáveis da tabela**|Informações do cache relacionadas a tabelas temporárias e tabelas variáveis.|  
  
## <a name="see-also"></a>Consulte Também  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, objeto Buffer Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
