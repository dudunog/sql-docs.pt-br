---
title: Logs de diagnóstico de integridade de DLL de recurso para grupos de disponibilidade
description: Descreve como a DLL de recurso do SQL Server monitora a integridade do Grupo de Disponibilidade AlwaysOn.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: how-to
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
ms.openlocfilehash: 72a023d4627d348421b392e8f787914edc986505
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643703"
---
# <a name="sql-server-resource-dll-health-diagnostic-logs-for-availability-groups"></a>Logs de diagnóstico de integridade de DLL de recurso do SQL Server para grupos de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Para monitorar a integridade da réplica de disponibilidade primária, a DLL de recurso do SQL Server executada pelo WSFC (Cluster de Failover do Windows Server) usa um procedimento armazenado na instância do SQL Server chamada [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).  
  
 A DLL de recurso do SQL Server mantém uma conexão aberta dedicada com a instância do SQL Server, por meio da qual a instância do SQL Server envia periodicamente um diagnóstico de integridade detalhado para a DLL de recurso do SQL Server. O diagnóstico de integridade, juntamente com a política de failover configurada no recurso do grupo de disponibilidade no cluster (a propriedade FailoverConditionLevel), é usado pelo cluster para determinar a necessidade de reinicializar ou de fazer failover do recurso do grupo de disponibilidade. Esse procedimento armazenado é "pulsação" da instância do SQL Server 2012 e posterior para o cluster WSFC, a qual é mais granular e confiável que no SQL Server 2008 R2 ou inferior, em que uma conexão periódica com a instância é feita com a consulta `SELECT @@SERVERNAME`. Assim, você pode controlar as condições que disparam failovers, definindo a propriedade FailureConditonLevel do grupo de disponibilidade.  
  
 **Usar os logs de diagnóstico do cluster de failover do SQL Server**
 
 Todos os diagnósticos de integridade que as DLLs de recurso do SQL Server recebem de sp_server_diagnostics são salvas automaticamente no diretório de Log padrão da instância do SQL Server (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log). Esses logs são conhecidos como logs SQLDIAG e são salvos no formato de arquivo XEL (eventos estendidos). Esses arquivos do diretório de Log do SQL Server têm o seguinte formato: \<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel. Ao examinar os logs SQLDIAG, você poderá determinar a causa raiz dos eventos de falha ou failover de recurso do grupo de disponibilidade.  
  
 Para exibir um log SQLDIAG, arraste o arquivo .xel até o SQL Server Management Studio.  
  
  
