---
title: Monitorar cluster com o Painel do Grafana
titleSuffix: SQL Server Big Data Clusters
description: Monitorar cluster com o Painel do Grafana no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ee0ceb3a9f86fc2a7fabe44e9279b7e63dabfb8b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091681"
---
# <a name="monitor-cluster-with-azdata-and-grafana-dashboard"></a>Monitorar cluster com o azdata e o Painel do Grafana

Este artigo descreve como monitorar um aplicativo em um Cluster de Big Data do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando azdata](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019, você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata bdc endpoint list` | Lista os pontos de extremidade para o cluster de Big Data. |


Use o exemplo a seguir para listar o ponto de extremidade do **Painel do Grafana**:

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

A saída fornecerá o ponto de extremidade, e você poderá usar o nome de usuário e a senha do cluster para fazer logon. 

![Painel do Grafana](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)

Os valores `nodeMetricsUrl` e `sqlMetricsUrl` são vinculados a um painel do Grafana para monitorar as métricas do nó do Kubernetes e as métricas de serviço de cluster de Big Data:

![Painel do grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)



## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).