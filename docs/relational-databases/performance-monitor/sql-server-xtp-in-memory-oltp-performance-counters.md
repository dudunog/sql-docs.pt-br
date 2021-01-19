---
title: Contadores de desempenho de XTP (OLTP na memória)
description: O SQL Server fornece objetos e contadores que podem ser usados pelo Monitor de Desempenho para monitorar a atividade OLTP in-memory.
ms.custom: seo-dt-2019
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 38d44cc0c916c7e40e26b89196b21012f7b72499
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98170708"
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Contadores de desempenho de XTP (OLTP na memória) do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor de Desempenho para monitorar a atividade OLTP in-memory. Os objetos e contadores são compartilhados entre todas as instâncias de determinada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador, a partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 No passado, os nomes de objeto e de contador começavam com *XTP*, como em **Cursores XTP**. Agora, a partir do [!INCLUDE[ssSQL15](../../includes/sssql16-md.md)], os nomes são parecidos com o seguinte padrão:  
  
-   **Cursores de XTP** do **SQL Server** *\<version>*  
  
 Para o *\<version>* , o valor é algo como 2016.  
  
##  <a name="sql-server-xtp-performance-objects"></a><a name="SQLServerPOs"></a> Objetos de desempenho XTP do SQL Server  
 A tabela a seguir descreve os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[Cursores de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|O objeto de desempenho Cursores de XTP do SQL Server contém os contadores relacionados aos cursores do mecanismo de XTP interno OLTP in-memory. Os cursores são os blocos de construção de baixo nível que o mecanismo OLTP In-Memory usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.|  
|[Bancos de dados XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|O objeto de desempenho Bancos de dados XTP do SQL Server fornece contadores específicos do banco de dados OLTP in-memory.|  
|[Coleta de Lixo de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|O objeto de desempenho Coleta de Lixo de XTP do SQL Server contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.|  
|[Administrador de E/S XTP do SQL Server 2016](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|O objeto de desempenho Administrador de E/S XTP do SQL Server contém contadores relacionados ao Administrador da Taxa de E/S do OLTP in-memory.|
|[Processador Fantasma de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|O objeto de desempenho Processador Fantasma de XTP do SQL Server contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo OLTP in-memory. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE.|  
|[Armazenamento de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|O objeto de desempenho Armazenamento XTP do SQL Server contém contadores relacionados ao armazenamento OLTP in-memory do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Log de transações de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|O objeto de desempenho do Log de Transações XTP do SQL Server contém contadores relacionados ao log de transações do OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transações XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|O objeto de desempenho do Log Transações XTP do SQL Server contém contadores relacionados às transações do mecanismo do OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
