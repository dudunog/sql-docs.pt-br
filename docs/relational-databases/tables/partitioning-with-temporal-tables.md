---
title: Particionamento com tabelas temporais | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc76e2a2aaee2d3bc8474c8cec06b7ee85a31971
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555881"
---
# <a name="partitioning-with-temporal-tables"></a>Particionamento com tabelas temporais

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Você pode usar o particionamento na tabela atual e de histórico de forma independente. No entanto, o particionamento não pode ser usado para alterar o conteúdo dos dados sem o controle da versão do sistema.

> [!NOTE]
> O particionamento é um recurso do Enterprise Edition no SQL Server 2016 antes do Service Pack 1 e versões anteriores. Há suporte para particionamento em todas as edições no SQL Server 2016 Service Pack 1 e versões posteriores.

- **Tabela atual:**

  - **SWITCH IN** na tabela atual para facilitar o carregamento de dados e a consulta enquanto o **SYSTEM_VERSIONING** estiver **ON**
  - **SWITCH OUT** não é permitido enquanto **SYSTEM_VERSIONING** estiver **ON**

- **Tabela de histórico:**

  - É possível executar o**SWITCH OUT** na tabela de hestivertórico enquanto o **SYSTEM_VERSIONING** estiver **ON** para limpar as partes dos dados de histórico que já não são relevantes.
  - Não há permestiversão para o**SWITCH IN** enquanto o **SYSTEM_VERSIONING** estiver **ON**, pois isso pode invalidar a consistência dos dados temporais.

## <a name="next-steps"></a>Próximas etapas

- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Introdução a tabelas temporais com controle da versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
