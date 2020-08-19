---
description: Criar rastreamentos manuais usando procedimentos armazenados
title: Criar rastreamentos manuais usando procedimentos armazenados
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d19212c30d7c9789b8e2ab3d42ccd3d4ac00bc0c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88402702"
---
# <a name="create-manual-traces-using-stored-procedures"></a>Criar rastreamentos manuais usando procedimentos armazenados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece procedimentos armazenados do sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar rastreamentos em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Esses procedimentos armazenados do sistema podem ser usados nos seus próprios aplicativos para criar rastreamentos manualmente em vez de usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Isso lhe permite escrever aplicativos personalizados específicos às necessidades de sua empresa.  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir lista os procedimentos armazenados do sistema para rastreamento de uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Procedimento armazenado|Tarefa executada|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|Retorna informações sobre eventos incluídos em um rastreamento.|  
|[sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|Retorna informações sobre um rastreamento especificado ou todos os rastreamentos existentes.|  
|[sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|Cria uma definição de rastreamento. O rastreamento novo estará em um estado interrompido.|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|Cria um evento definido pelo usuário.|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|Adiciona ou remove uma classe de evento ou coluna de dados de um rastreamento.|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|Inicia, interrompe ou encerra um rastreamento.|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|Retorna informações sobre filtros aplicados a um rastreamento.|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|Aplica um filtro novo ou modificado a um rastreamento.|  
  
 **Para definir seu próprio rastreamento usando procedimentos armazenados**  
  
1.  Especifique os eventos a serem capturados usando **sp_trace_setevent**.  
  
2.  Especifique qualquer filtro de evento. Para obter mais informações, veja [Definir um filtro de rastreamento #40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md).  
  
3.  Especifique o destino para os dados do evento capturado usando **sp_trace_create**.  

 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **Para definir padrões de definição de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **Para definir padrões de exibição de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Para criar um rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **Para adicionar ou remover eventos de um modelo de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
