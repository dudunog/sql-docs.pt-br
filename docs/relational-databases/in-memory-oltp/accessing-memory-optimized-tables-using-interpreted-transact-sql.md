---
title: Tabelas com otimização de memória usando T-SQL interpretado
description: Saiba mais sobre como acessar tabelas com otimização de memória usando Transact-SQL interpretados (lotes do Transact-SQL ou procedimentos armazenados no SQL Server).
ms.custom: seo-dt-2019
ms.date: 05/31/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d61c6e1ebb1d417ebe3f95f588a1e2b12b6b5f3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246261"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Acessando tabelas com otimização de memória usando Transact-SQL interpretado
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

 Com raras exceções, você pode acessar tabelas com otimização de memória usando qualquer consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] ou operação DML (seleção, inserção, atualização ou exclusão), lotes ad hoc e os módulos SQL, como procedimentos armazenados, funções com valor de tabela, gatilhos e exibições.  
  
O [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado se refere a lotes ou a procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] , que não sejam um procedimento armazenado nativamente compilado. O acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado às tabelas com otimização de memória é conhecido como acesso de interoperabilidade.  

A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], as consultas em [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado podem examinar tabelas com otimização de memória em paralelo, em vez de apenas em modo serial.

As tabelas com otimização de memória também podem ser acessadas usando um procedimento armazenado compilado nativamente. Os procedimentos armazenados nativamente compilados são recomendados para operações OLTP de desempenho crítico.  
  
O acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado é recomendado para estes cenários:  
  
- Consultas ad hoc e tarefas administrativas.  
  
- As consultas de relatórios, que tipicamente usam construções não disponíveis em procedimentos armazenados compilados de modo nativo (como funções *window* , às vezes chamadas de funções [OVER](../../t-sql/queries/select-over-clause-transact-sql.md) ).  
  
- Para migrar partes críticas de desempenho do aplicativo para as tabelas com otimização de memória, com alterações mínimas (ou não) do código do aplicativo. Potencialmente, você pode ver aprimoramentos de desempenho de tabelas de migração. Se então você migrar procedimentos armazenados para procedimentos armazenados nativamente compilados, talvez veja mais aprimoramento de desempenho.  
  
- Quando uma declaração do [!INCLUDE[tsql](../../includes/tsql-md.md)] não estiver disponível para procedimentos armazenados nativamente compilados.  
  
Entretanto, as seguintes construções do [!INCLUDE[tsql](../../includes/tsql-md.md)] não têm suporte em procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado que acessam dados em uma tabela com otimização de memória.  
  
|Área|Sem suporte|  
|----------|-----------------|  
|Acesso a tabelas|TRUNCATE TABLE<br /><br /> MERGE (tabela com otimização de memória como destino).<br /><br /> Cursores de conjunto de chaves e dinâmicos (degradados automaticamente para estáticos).<br /><br /> Acesso dos módulos CLR, usando a conexão de contexto.<br /><br /> Referenciando uma tabela com otimização de memória de uma exibição indexada.|  
|Entre bancos de dados|Consultas de bancos de dados<br /><br /> Transações entre bancos de dados<br /><br /> Servidores vinculados|  
  
## <a name="table-hints"></a>Dicas de tabela

Para obter mais informações sobre dicas de tabela, consulte. [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md). O SNAPSHOT foi adicionado para oferecer suporte a [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
As dicas de tabela a seguir não têm suporte para acessar uma tabela com otimização de memória usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado.  

:::row:::
    :::column:::
        HOLDLOCK

        PAGLOCK

        READUNCOMMITTED

        TABLOCKXX
    :::column-end:::
    :::column:::
        IGNORE_CONSTRAINTS

        READCOMMITTED

        ROWLOCK

        UPDLOCK
    :::column-end:::
    :::column:::
        IGNORE_TRIGGERS

        READCOMMITTEDLOCK

        SPATIAL_WINDOW_MAX_CELLS = *integer*

        XLOCK
    :::column-end:::
    :::column:::
        NOWAIT

        READPAST

        TABLOCK
    :::column-end:::
:::row-end:::

Ao acessar uma tabela com otimização de memória de uma transação explícita ou implícita usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado, é necessário seguir, pelo menos, uma das seguintes opções:  
  
- Especificar uma [dica de tabela de nível de isolamento](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) como SNAPSHOT, REPEATABLEREAD ou SERIALIZABLE.  
  
- Configurar a opção de banco de dados [MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT](../../t-sql/statements/alter-database-transact-sql-set-options.md) como ON.  
  
Uma dica de tabela de nível de isolamento não é necessária para tabelas com otimização de memória acessadas por consultas executadas no [modo de confirmação automática](https://msdn.microsoft.com/c8de5b60-d147-492d-b601-2eeae8511d00).  
  
## <a name="see-also"></a>Consulte Também

[Suporte ao Transact-SQL para OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   

[Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

