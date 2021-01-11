---
title: O que é o PolyBase? | Microsoft Docs
description: O PolyBase permite que sua instância do SQL Server processe consultas Transact-SQL que leem dados de fontes de dados externas como o Hadoop e o Armazenamento de Blobs do Azure.
ms.date: 12/14/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
ms.custom: contperf-fy21q2
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: afcc848a169ec6a9c9dd02ecee50718d7e1508c1
ms.sourcegitcommit: 81f06a754fcaf4b72136859ccb18c82693f24780
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97811531"
---
# <a name="what-is-polybase"></a>O que é o PolyBase?

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

O PolyBase permite que a instância do SQL Server processe consultas Transact-SQL que leem dados de fontes de dados externas. A mesma consulta também pode acessar tabelas relacionais na sua instância do SQL Server. O PolyBase permite que a mesma consulta também una os dados de fontes externas e do SQL Server.

Para usar o PolyBase, em uma instância do SQL Server:

1. [Instalar o PolyBase no Windows](polybase-installation.md)
1. Criar uma [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md)
1. Criar uma [tabela externa](../../t-sql/statements/create-external-table-transact-sql.md)

Juntos, elas fornecem a conexão com a fonte de dados externa.

O SQL Server 2016 apresenta o PolyBase com suporte para conexões com o Hadoop e o Armazenamento de Blobs do Azure.

O SQL Server 2019 apresenta conectores adicionais, incluindo o SQL Server, o Oracle, o Teradata e o MongoDB.

![PolyBase lógico](../../relational-databases/polybase/media/polybase-logical.png "PolyBase lógico")

O PolyBase envia alguns cálculos para a fonte externa a fim de otimizar a consulta geral. O acesso externo do PolyBase não é limitado ao Hadoop. Outras tabelas relacionais não estruturadas também são suportadas, como arquivos de texto delimitado.

Entre os exemplos de conectores externos estão:

- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)

### <a name="supported-sql-products-and-services"></a>Produtos e serviços SQL compatíveis

O PolyBase fornece essas mesmas funcionalidades para os seguintes produtos SQL da Microsoft:

- SQL Server 2016 e verões posteriores (somente Windows)
- O Analytics Platform System (anteriormente conhecido como Parallel Data Warehouse)
- Azure Synapse Analytics

### <a name="azure-integration"></a>Integração do Azure

Com a Ajuda subjacente do PolyBase, consultas T-SQL também podem importar e exportar dados do Armazenamento de Blobs do Azure. Além disso, o PolyBase permite que o Azure Synapse Analytics importe e exporte dados do Armazenamento de Blobs do Azure e do Azure Data Lake Store.

## <a name="why-use-polybase"></a>Por que usar o PolyBase?

O PolyBase permite que você una dados de uma instância do SQL Server com os dados externos. Antes de o PolyBase unir os dados com fontes de dados externas, você pode:

- Transferir metade dos dados para que todos os dados estejam em uma só localização.
- Consultar ambas as fontes de dados, então escrever lógica de consulta personalizada para ingressar e integrar os dados no nível do cliente.

O PolyBase permite que você simplesmente use o Transact-SQL para unir os dados.

O PolyBase não exige a instalação de software adicional no ambiente do Hadoop. Você pode consultar dados externos usando a mesma sintaxe do T-SQL usada para consultar uma tabela de banco de dados. As ações de suporte implementadas pelo PolyBase todos ocorrem de maneira transparente. O autor da consulta não precisa ter nenhum conhecimento sobre a fonte externa.

### <a name="polybase-uses"></a>Usos do PolyBase

O PolyBase habilita os seguintes cenários no SQL Server:

- **Consultar os dados armazenados no Hadoop por meio de uma instância do SQL Server ou do PDW.** Os usuários estão armazenando dados em sistemas escalonáveis e distribuídos mais econômicos, como o Hadoop. O PolyBase facilita a consulta dos dados com T-SQL.

- **Consulte os dados armazenados no Armazenamento de Blobs do Azure.** O armazenamento de blobs do Azure é um local conveniente para armazenar dados para uso dos serviços do Azure.  O PolyBase facilita o acesso aos dados com T-SQL.

- **Importe dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store.** Aproveite a velocidade das funcionalidades de análise e tecnologia de columnstore do Microsoft SQL, com a importação de dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store em tabelas relacionais. Não é necessário ter uma ferramenta separada de ETL ou importação.

- **Exporte dados para o Hadoop, o Armazenamento de Blobs do Azure ou o Azure Data Lake Store.** Arquive dados no Hadoop, no Armazenamento de Blobs do Azure ou no Azure Data Lake Store para obter um armazenamento econômico e mantê-los online para fácil acesso.

- **Integre com ferramentas de BI.** Use o PolyBase com a business intelligence e a pilha de análise da Microsoft ou use as ferramentas de terceiros compatíveis com o SQL Server.

## <a name="performance"></a>Desempenho

- **Enviar por push de computação para Hadoop.** O otimizador de consulta toma a decisão baseada em custo de enviar por push a computação para o Hadoop, caso isso aprimore o desempenho de consulta.  O otimizador de consulta usa as estatísticas nas tabelas externas para tomar a decisão baseada em custo. O envio por push do cálculo cria trabalhos MapReduce e aproveita os recursos computacionais distribuídos do Hadoop.

- **Escale os recursos de computação.** Para melhorar o desempenho da consulta, é possível usar os [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)do SQL Server. Isso permite a transferência de dados em paralelo entre as instâncias do SQL Server e os nós do Hadoop, além de adicionar recursos de computação para operação em dados externos.

## <a name="next-steps"></a>Próximas etapas

Antes de usar o PolyBase, é preciso [instalar o recurso do PolyBase](polybase-installation.md). Em seguida, confira os guias de configuração a seguir, dependendo da sua fonte de dados:

- [Hadoop](polybase-configure-hadoop.md)
- [Armazenamento de Blobs do Azure](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [Tipos genéricos de ODBC](polybase-configure-odbc-generic.md)