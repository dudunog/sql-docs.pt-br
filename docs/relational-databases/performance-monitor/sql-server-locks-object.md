---
title: SQL Server, objeto Bloqueios | Microsoft Docs
description: Saiba mais sobre o objeto SQLServer:Locks, que fornece informações sobre bloqueios do SQL Server em tipos de recurso individuais.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 94e726a108c78ffec8715e80c4b14f2274656be0
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505660"
---
# <a name="sql-server-locks-object"></a>SQL Server, objeto Locks
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto **SQLServer:Locks** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece informações sobre bloqueios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipos de recurso individuais. Os bloqueios são mantidos nos recursos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como linhas lidas ou modificadas durante uma transação, para evitar o uso simultâneo de recursos por transações diferentes. Por exemplo, se um bloqueio exclusivo (X) for mantido em uma linha de uma tabela por uma transação, nenhuma outra transação poderá modificar essa linha até que o bloqueio seja liberado. Minimizar bloqueios aumenta a simultaneidade, o que pode melhorar o desempenho. Várias instâncias do objeto **Locks** podem ser monitoradas ao mesmo tempo, com cada instância representando um bloqueio em um tipo de recurso.  
  
 Esta tabela descreve os contadores **Bloqueios** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores Locks do SQL Server|Descrição|  
|-------------------------------|-----------------|  
|**Tempo de Espera Médio (ms)**|Tempo médio de espera (em milissegundos) de cada solicitação de bloqueio que resultou em uma espera.|  
|**Base do tempo de espera médio**|Apenas para uso interno.|
|**Solicitações de Bloqueio/s**|Número de bloqueios novos e conversões de bloqueio, por segundo, solicitados a partir do gerenciador de bloqueios.|  
|**Tempos Limite de Bloqueio (tempo limite > 0)/s**|Número de solicitações de bloqueio, por segundo, que ultrapassaram o tempo limite, excluindo-se solicitações de bloqueios NOWAIT.|  
|**Tempos Limite de Bloqueio/s**|Número de solicitações de bloqueio, por segundo, que ultrapassaram o tempo limite, inclusive solicitações de bloqueios NOWAIT.|  
|**Tempo de Espera de Bloqueio (ms)**|Tempo de espera total (em milissegundos) dos bloqueios no último segundo.|  
|**Esperas de Bloqueio/s**|Número de solicitações de bloqueio, por segundo, que exigiram que o chamador esperasse.|  
|**Número de Deadlocks/s**|Número de solicitações de bloqueio, por segundo, que resultaram em um deadlock.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode bloquear esses recursos.  
  
|Item|Descrição|  
|----------|-----------------|  
|**_Total**|Informações de todos os bloqueios.|  
|**AllocUnit**|Um bloqueio em uma unidade de alocação.|  
|**Aplicativo**|Um bloqueio em um recurso especificado por aplicativo.|  
|**Backup de banco de dados**|Um bloqueio em um banco de dados, inclusive todos os seus objetos.|  
|**Extensão**|Um bloqueio em um grupo contíguo de 8 páginas.|  
|**Arquivo**|Um bloqueio em um arquivo de banco de dados.|  
|**Heap/BTree**|Heap ou BTree (HOBT). Um bloqueio em um heap de páginas de dados ou na estrutura BTree de um índice.|  
|**Chave**|Um bloqueio em uma linha de um índice.|  
|**Metadados**|Um bloqueio em uma parte das informações de catálogo, também chamadas de metadados.|  
|**Objeto**|Um bloqueio em tabela, procedimento armazenado, exibição, etc, inclusive todos os dados e índices. O objeto pode ser qualquer coisa que tenha uma entrada em **sys.all_objects**.|  
|**Página**|Um bloqueio em uma página de 8 quilobytes (KB) em um banco de dados.|  
|**RID**|ID de linha. Um bloqueio em uma única linha de um heap.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
