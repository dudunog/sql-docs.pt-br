---
title: Confira os logs de cluster com o painel do Kibana
titleSuffix: SQL Server Big Data Clusters
description: Monitoramento de cluster com o Painel do Kibana no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 55dc3056b9f66f7a96b55ab750a5f74fe9bfd394
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091706"
---
# <a name="check-out-cluster-logs--with-kibana-dashboard"></a>Confira os logs de cluster com o painel do Kibana

Este artigo descreve como monitorar um aplicativo em um Cluster de Big Data do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando azdata](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019, você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata bdc endpoint list` | Lista os pontos de extremidade para o cluster de Big Data. |


Use o seguinte exemplo para listar o ponto de extremidade do **painel do Kibana**:

```bash
azdata bdc endpoint list --endpoint-name logsui 
```

A saída fornecerá o ponto de extremidade, e você poderá usar o nome de usuário e a senha do cluster para fazer logon. 

![Painel do Kibana](media/big-data-cluster-monitor-cluster/kibana-dashboard-endpoint.png)


O link para um painel do Kibana:

![Painel do kibana](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> (Antigo) O navegador Microsoft Edge é incompatível com o Kibana, você precisa usar o navegador baseado em Chrome para que o painel seja exibido corretamente. Você verá uma página em branco ao carregar os painéis usando um navegador sem suporte. Confira aqui os navegadores compatíveis com o Kibana.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).