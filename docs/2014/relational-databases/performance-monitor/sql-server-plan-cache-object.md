---
title: SQL Server, objeto Cache de planos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bf5fbc6c3a01b39079c8f63a2998490025c85e8c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066927"
---
# <a name="sql-server-plan-cache-object"></a>SQL Server, objeto Cache de planos
  O objeto **Plan Cache** fornece contadores para monitorar como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a memória para armazenar objetos, como procedimentos armazenados e instruções e gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc e preparados. Diversas instâncias do objeto **Plan Cache** podem ser monitoradas ao mesmo tempo, com cada instância representando um tipo de plano diferente para monitorar.  
  
 Esta tabela descreve os contadores **SQLServer:Plan Cache**.  
  
|Contadores SQL Server Plan Cache|DESCRIÇÃO|  
|------------------------------------|-----------------|  
|**Taxa de Acertos do Cache**|Taxa entre acertos e pesquisas do cache.|  
|**Contagens de objetos de cache**|Número de objetos do cache no cache.|  
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
 [Opções de configuração de servidor de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, objeto Gerenciador de buffer](sql-server-buffer-manager-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
