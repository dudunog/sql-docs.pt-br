---
title: Transações XTP do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b8da1956665775cf54da529140a10a8477cd86ad
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85741522"
---
# <a name="sql-server-xtp-transactions"></a>Transações XTP do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O objeto de desempenho do Log Transações XTP do SQL Server contém contadores relacionados às transações que envolvem OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores **Transações de XTP do SQL Server** .  
  
|Contador|DESCRIÇÃO|  
|-------------|-----------------|  
|**Anulações em cascata/s**|O número de transações que foram revertidas devido a uma reversão de dependência de confirmação (em média), por segundo.|  
|**Dependências de confirmação realizadas/s**|O número de dependências de confirmação realizadas por transações (em média), por segundo.|  
|**Transações somente leitura preparadas/s**|O número de transações somente leitura que foram preparadas para o processamento da confirmação, por segundo.|  
|**Atualizações de ponto de salvamento/s**|O número de vezes que um ponto de salvamento foi “atualizado”, (em média), por segundo. Uma atualização de ponto de salvamento é quando um ponto de salvamento existente é redefinido para o momento atual no tempo de vida da transação.|  
|**Reversões de ponto de salvamento/s**|O número de vezes que uma transação foi revertida para um ponto de salvamento (em média), por segundo.|  
|**Pontos de salvamento criados/s**|O número de pontos de salvamento criados (em média), por segundo.|  
|**Falha de validação de transação/s**|O número de transações que falharam no processamento de validação (em média), por segundo.|  
|**Transações anuladas por usuário/s**|O número de transações que foram anuladas pelo usuário (em média), por segundo.|  
|**Transações anuladas/s**|O número de transações que foram anuladas (pelo usuário e pelo sistema) em média, por segundo.|  
|**Transações criadas/s**|O número de transações criadas no sistema (em média), por segundo.<br /><br /> As transações de XTP são contadas diferentemente de transações baseadas em disco (conforme refletido em bancos de dados:transações/s). Por exemplo, transações criadas/s contam como transações somente leitura, mas isso não ocorre com bancos de dados:transações/s.|  
  
## <a name="see-also"></a>Consulte Também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
