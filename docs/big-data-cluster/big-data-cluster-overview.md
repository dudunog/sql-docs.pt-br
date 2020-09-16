---
title: O que são Clusters de Big Data?
titleSuffix: SQL Server Big Data Clusters
description: Saiba mais sobre os Clusters de Big Data do SQL Server que são executados no Kubernetes e fornecem opções de expansão para dados relacionais e do HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d21f5c3f572356a18f8567f798af8af10f58c001
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765735"
---
# <a name="what-are-big-data-clusters-2019"></a>O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

No [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] em diante, os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] permitem implantar clusters escalonáveis de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. Esses componentes são executados lado a lado para permitir que você leia, grave e processe Big Data do Transact-SQL ou do Spark, permitindo combinar e analisar facilmente seus dados relacionais de alto valor com Big Data de alto volume.

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta os Clusters de Big Data do SQL Server.

Use Clusters de Big Data do SQL Server para:

- [Implantar clusters escalonáveis](./deploy-get-started.md) de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. 
- Ler, gravar e processar Big Data do Transact-SQL ou do Spark.
- Combine e analise facilmente dados relacionais de valor elevado com Big Data de volume grande.
- Consultar fontes de dados externas.
- Armazenar Big Data no HDFS gerenciado por SQL Server.
- Consultar dados de várias fontes de dados externas por meio do cluster.
- Usar os dados para IA, aprendizado de máquina e outras tarefas de análise.
- [Implantar e executar aplicativos](./concept-application-deployment.md) em [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)].
- Virtualizar dados com o [PolyBase](../relational-databases/polybase/polybase-guide.md). Consulte dados de SQL Server externos, Oracle, Teradata, MongoDB e fontes de dados ODBC com tabelas externas.
- Forneça alta disponibilidade para a instância mestra do SQL Server e todos os bancos de dados usando a tecnologia de grupo de disponibilidade Always On.

Para obter mais informações sobre os novos recursos e problemas conhecidos da versão mais recente, confira as [notas sobre a versão](release-notes-big-data-cluster.md).

## <a name="scenarios"></a>Cenários

Os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] fornecem flexibilidade na maneira como você interage com Big Data. Você pode consultar fontes de dados externas, armazenar Big Data no HDFS gerenciado pelo SQL Server ou consultar dados de várias fontes de dados externas por meio do cluster. Depois, você pode usar os dados para IA, aprendizado de máquina e outras tarefas de análise. As seções a seguir fornecem mais informações sobre estes cenários.

### <a name="data-virtualization"></a>Virtualização de dados

Utilizando o [SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] podem consultar fontes de dados externas sem mover nem copiar os dados. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta novos conectores para fontes de dados.

![Virtualização de dados](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Um cluster de Big Data do SQL Server inclui um *pool de armazenamento* do HDFS escalonável. Ele pode ser usado para armazenar Big Data, potencialmente ingerido de várias fontes externas. Após o Big Data ser armazenado no HDFS no cluster de Big Data, você poderá analisar e consultar os dados e combiná-los com os dados relacionais.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Data mart de expansão

Os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] fornecem computação e armazenamento de expansão para melhorar o desempenho da análise de dados. Dados de diversas origens podem ser ingeridos e distribuídos entre nós do *pool de dados* como um cache para análise posterior.

![Data mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>IA e aprendizado de máquina integrados

Os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] habilitam tarefas de IA e de aprendizado de máquina nos dados armazenados em pools de armazenamento HDFS e nos pools de dados. Você pode usar o Spark, bem como ferramentas internas de IA no SQL Server, usando R, Python, Scala ou Java.

![IA e ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

O gerenciamento e o monitoramento são fornecidos por meio de uma combinação de ferramentas de linha de comando, APIs, portais e exibições de gerenciamento dinâmico.

É possível usar o [Azure Data Studio](../azure-data-studio/what-is.md) para executar uma variedade de tarefas no cluster de Big Data:
- Snippets internos para tarefas comuns de gerenciamento.
- Capacidade de navegar no HDFS, carregar arquivos, visualizar arquivos e criar diretórios.
- Capacidade de criar, abrir e executar notebooks compatíveis com Jupyter.
- Assistente de virtualização de dados para simplificar a criação de fontes de dados externas (habilitadas pela **Extensão de Virtualização de Dados**).

## <a name="architecture"></a><a id="architecture"></a> Arquitetura

Um cluster de Big Data do SQL Server é um cluster de contêineres Linux orquestrados pelo [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceitos do Kubernetes

O Kubernetes é um orquestrador de contêineres de software livre que pode dimensionar implantações de contêiner de acordo com a necessidade. A tabela a seguir define algumas terminologias importantes do Kubernetes:

|Termo|Descrição|
|:--|:--|
| **Cluster** | Um cluster do Kubernetes é um conjunto de computadores, conhecidos como nós. Um nó controla o cluster e é designado como nó mestre; os nós restantes são nós de trabalho. O mestre do Kubernetes é responsável por distribuir o trabalho entre os trabalhadores e por monitorar a integridade do cluster. |
| **Nó** | Um nó executa aplicativos em contêineres. Ele pode ser um computador físico ou uma máquina virtual. Um cluster do Kubernetes pode conter uma combinação de nós de computadores físicos e de máquinas virtuais. |
| **Pod** | Um pod é a unidade de implantação atômica do Kubernetes. Um pod é um grupo lógico de um ou mais contêineres – e recursos associados – necessários para executar um aplicativo. Cada pod é executado em um nó; um nó pode executar um ou mais pods. O mestre do Kubernetes atribui pods automaticamente aos nós no cluster. |
| &nbsp; ||

Nos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], o Kubernetes é responsável pelo estado dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]. O Kubernetes compila e configura os nós do cluster, atribui pods aos nós e monitora a integridade do cluster.

### <a name="big-data-clusters-architecture"></a>Arquitetura de clusters de Big Data

O diagrama a seguir mostra os componentes de um cluster de Big Data para o SQL Server.

![Visão geral da arquitetura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a name="controller"></a><a id="controlplane"></a> Controlador

O controlador fornece gerenciamento e segurança para o cluster. Ele contém o serviço de controle, o repositório de configurações e outros serviços no nível do cluster, como Kibana, Grafana e Pesquisa Elástica.

### <a name="compute-pool"></a><a id="computeplane"></a> Pool de computação

O pool de computação fornece recursos computacionais para o cluster. Ele contém nós que executam pods do SQL Server em Linux. Os pods no pool de computação são divididos em *instâncias de computação do SQL* para tarefas de processamento específicas. 

### <a name="data-pool"></a><a id="dataplane"></a> Pool de dados

O pool de dados é usado para persistência e cache de dados. O pool de dados é composto por um ou mais pods em execução no SQL Server em Linux. Ele é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. Data marts do cluster de Big Data do SQL Server são persistidos no pool de dados. 

### <a name="storage-pool"></a>Pool de armazenamento

O pool de armazenamento é composto por pods do pool de armazenamento compostos pelo SQL Server em Linux, pelo Spark e pelo HDFS. Todos os nós de armazenamento em um cluster de Big Data do SQL Server são membros de um cluster do HDFS.

> [!TIP]
> Para obter uma análise detalhada da arquitetura e da instalação do cluster de Big Data, confira [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/microsoft/sqlworkshops-bdc).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como implantar Clusters de Big Data do SQL Server, confira [Introdução aos Clusters de Big Data do SQL Server](deploy-get-started.md).