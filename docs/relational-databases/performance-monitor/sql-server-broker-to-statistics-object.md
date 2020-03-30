---
title: SQL Server, objeto Estatísticas TO do Agente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6485a99d759d4c4b09ec2b78946f7e1aecd46204
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67986972"
---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server, objeto Broker TO Statistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho SQLServer:Broker TO Statistics informa quantas vezes os diálogos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] requerem objetos de transmissão, e com que frequência os objetos de transmissão são gravados no **tempdb**.  
  
 Objetos de transmissão registram o estado de transmissões de mensagem para um diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Eles são armazenados na memória. Para liberar a memória, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] grava lotes de objetos de transmissão inativos periodicamente em tabelas de trabalho no **tempdb**.  
  
 A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server Broker TO Statistics|Descrição|  
|----------------------------------------------|-----------------|  
|**Méd. de gravações em lotes**|O número médio de objetos de transmissão salvo em um lote.|  
|**Méd. de tempo de gravação em lote (ms)**|O número médio de milissegundos exigido para salvar um lote de objetos de transmissão.|  
|**Méd. de tempo de base de gravação em lote**|Apenas para uso interno.|
|**Méd. de tempo entre lotes (ms)**|O número médio de milissegundos entre gravações de lotes de objetos de transmissão.|  
|**Méd. de tempo entre as base de lotes**|Apenas para uso interno.| 
|**Obtenções de Objeto de Transmissão/s**|O número de vezes por segundo que os diálogos solicitaram objetos de transmissão.|  
|**Objetos de Transmissão Marcados como Sujos/s**|O número de vezes por segundo que objetos de transmissão foram marcados como sujos. Os objetos de transmissão são marcados como sujos pela primeira modificação que faz com que a cópia na memória se diferencie da cópia armazenada no **tempdb**. Objetos de transmissão são modificados quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] precisa registrar uma alteração no estado das transmissões das mensagens para o diálogo.|  
|**Gravações de Objetos de Transmissão/s**|O número de vezes por segundo que um lote de objetos de transmissão foi gravado nas tabelas de trabalho do **tempdb** . Gravações em grande número podem indicar que a memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo pressionada.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server, Objeto Métodos de Acesso](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [SQL Server, objeto Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
