---
title: Configurar a instância mestra do SQL Server
titleSuffix: Configure SQL Server master instance of Big Data Cluster
description: Configurar a instância mestra de um cluster de Big Data do SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3937152161cdfb1124c8761c61ac20cb7218b9d8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784342"
---
# <a name="configure-master-instance-of-big-data-clusters-2019"></a>Configurar a instância mestra do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Configure a instância mestra do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

As definições de configuração do servidor não podem ser configuradas para a instância mestra do SQL Server no momento da implantação. Este artigo descreve uma solução alternativa temporária de como definir configurações como a edição do SQL Server, habilitar ou desabilitar o SQL Server Agent, habilitar sinalizadores de rastreamento específicos ou habilitar/desabilitar comentários do cliente.

Para alterar uma dessas configurações, siga estas etapas:

1. Crie um arquivo `mssql-custom.conf` personalizado que inclua as configurações de destino. O seguinte exemplo habilita o SQL Agent, a telemetria, define um PID para a Edição Enterprise e habilita o sinalizador de rastreamento 1204:

   ```
   [sqlagent]
   enabled=true
   
   [telemetry]
   customerfeedback=true
   userRequestedLocalAuditDirectory = /tmp/audit

   [DEFAULT]
   pid = Enterprise

   [traceflag]
   traceflag0 = 1204
   ```

1. Copie o arquivo `mssql-custom.conf` para `/var/opt/mssql` no contêiner `mssql-server` no pod `master-0`. Substitua `<namespaceName>` pelo nome do cluster de Big Data.

   ```bash
   kubectl cp mssql-custom.conf master-0:/var/opt/mssql/mssql-custom.conf -c mssql-server -n <namespaceName>
   ```

1. Reinicie a Instância do SQL Server.  Substitua `<namespaceName>` pelo nome do cluster de Big Data.

   ```bash
   kubectl exec -it master-0  -c mssql-server -n <namespaceName> -- /bin/bash
   supervisorctl restart mssql-server
   exit
   ```

> [!IMPORTANT]
> Se a instância mestra do SQL Server estiver em uma configuração de grupos de disponibilidade, copie o arquivo `mssql-custom.conf` em todos os pods `master`. Observe que cada reinicialização causará um failover, portanto, você precisa verificar se está cronometrando essa atividade durante períodos de tempo de inatividade.

## <a name="known-limitations"></a>Limitações conhecidas

- As etapas acima exigem permissões de administrador do cluster do Kubernetes
- Não é possível alterar a ordenação do servidor na instância mestra do SQL Server do cluster de Big Data após a implantação.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como implantar Clusters de Big Data do SQL Server, confira [Introdução aos Clusters de Big Data do SQL Server](deploy-get-started.md).