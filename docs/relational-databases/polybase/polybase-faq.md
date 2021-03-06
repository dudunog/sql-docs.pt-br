---
title: Perguntas frequentes no PolyBase | Microsoft Docs
description: Faça a comparação do PolyBase com servidores vinculados e do PolyBase em Clusters de Big Data e em instâncias autônomas. Descubra as novidades no PolyBase 2019.
ms.date: 12/02/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.openlocfilehash: 57d59e774c1042bf7989bcd2df4a652ed4498f0d
ms.sourcegitcommit: 7a3fdd3f282f634f7382790841d2c2a06c917011
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563132"
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="polybase-vs-linked-servers"></a>PolyBase VS. servidores vinculados
A tabela a seguir destaca as diferenças entre o PolyBase e os recursos de servidor vinculado:

|PolyBase | Servidores vinculados|
|--------------------------|--------------------------|  
|Objeto no escopo do banco de dados|Objeto no escopo da instância|
|Usa drivers ODBC|Usa provedores OLE DB|
|Oferece suporte a operações somente leitura para todas as fontes de dados e a operação de inserção para HADOOP e fonte de dados de pool de dados somente|Oferece suporte a operações de leitura e gravação|
|Consultas à fonte de dados remota de uma única conexão podem ser expandidas |Consultas à fonte de dados remota de uma única conexão não podem ser expandidas|
|Há suporte para a propagação de predicados|Há suporte para a propagação de predicados|
|Nenhuma configuração separada é necessária para o grupo de disponibilidade|Configuração separada necessária para cada instância no grupo de disponibilidade|
|Somente autenticação básica|Autenticação básica e integrada|
|Adequado para consultas analíticas que processam um grande número de linhas|Adequado para consultas OLTP que retornam uma ou algumas linhas|
|Consultas que usam tabela externa não podem participar de transações distribuídas|Consultas distribuídas podem participar de transações distribuídas|

## <a name="whats-new-in-polybase-2019"></a>Quais são as novidades no PolyBase 2019? 

O PolyBase no [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] agora pode ler dados de uma maior variedade de fontes de dados. Os dados dessas fontes de dados externas podem ser armazenados como tabelas externas no SQL Server. O PolyBase também dá suporte à computação de aplicação para essas fontes de dados externas, exceto tipos genéricos de ODBC.

### <a name="compatible-data-sources"></a>Fontes de dados compatíveis

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipos genéricos de ODBC compatíveis
  
> [!NOTE]
> O PolyBase pode permitir a conexão a fontes de dados externas usando drivers ODBC de terceiros. Esses drivers não são fornecidos com o PolyBase e podem não funcionar conforme o esperado. Para obter mais informações, veja nosso [guia](../../relational-databases/polybase/polybase-configure-odbc-generic.md) para configuração genérica do PolyBase ODBC.  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>PolyBase em Clusters de Big Data vs. PolyBase em Instâncias autônomas

A tabela a seguir destaca os recursos do PolyBase disponíveis na instalação autônoma do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e no cluster de Big Data do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]:

|Recurso |Cluster de Big Data|Instância autônoma|
|--------------------------|--------------------------|---------|   
|Criar fonte de dados externa para SQL Server, Oracle, Teradata e Mongo DB |X|X|
|Criar fonte de dados externa usando um Driver ODBC de terceiros compatível | | X|
|Criar fonte de dados externa para a fonte de dados do HADOOP | X| X|
|Criar fonte de dados externa para o Armazenamento de Blobs do Azure | X| X|
|Criar tabela externa em um pool de dados do SQL Server | X| |
|Criar tabela externa em um pool de armazenamento do SQL Server | X| |
|Expandir execução de consulta | X| X (somente Windows) |

> [!NOTE]
>A tabela não descreve a funcionalidade disponível na última CTP do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]. Para conhecer os recursos disponíveis, confira as notas sobre a versão. Para obter mais informações sobre conexões usando o conector genérico ODBC, acesse nosso [Guia de instruções para configurar os tipos genéricos de ODBC](polybase-configure-odbc-generic.md).
