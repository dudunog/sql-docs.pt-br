---
title: Mestre do Scale Out | Microsoft Docs
description: Este artigo descreve o componente Scale Out Master do SSIS Scale Out
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: e7d9bc5b6d84a0108fd68a77a06bcbda5bf47d44
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918992"
---
# <a name="integration-services-ssis-scale-out-master"></a>Mestre de Expansão de Integration Services (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



O Mestre do Scale Out gerencia o sistema do Scale Out por meio do Catálogo do SSISDB e do serviço Mestre do Scale Out. 

O Catálogo do SSISDB armazena todas as informações de Trabalhos do Scale Out, pacotes e execuções. Ele fornece a interface para habilitar um Trabalho de Expansão e executar pacotes em Expansão. Saiba mais no [Passo a passo: configurar o Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md) e [Executar pacotes no Integration Services](run-packages-in-integration-services-ssis-scale-out.md).

O serviço Mestre do Scale Out é um serviço Windows responsável pela comunicação com os Trabalhos do Scale Out. Ele retorna o status das execuções de pacote nos Trabalhos do Scale Out por HTTPS e opera nos dados no SSISDB. 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>Exibições e procedimentos armazenados do Scale Out no SSISDB

### <a name="views"></a>Exibições

- [[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
- [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)

### <a name="stored-procedures"></a>Procedimentos armazenados

- Para gerenciar Trabalhos do Scale Out:
    - [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    - [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)

- Para executar pacotes na Escala horizontal:
    - [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    - [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    - [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)

## <a name="configure-the-scale-out-master-service"></a>Configurar o serviço Mestre do Scale Out

Configure o serviço Mestre do Scale Out usando o arquivo `<drive>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`. É necessário reiniciar o serviço depois de atualizar o arquivo de configuração.


|Configuração  |Descrição  |Valor Padrão  |
|---------|---------|---------|
|PortNumber|O número da porta de rede usado para se comunicar com um Trabalho de Expansão.|8391|
|SSLCertThumbprint|A impressão digital do certificado TLS/SSL usado para proteger a comunicação com um Trabalho do Scale Out.|A impressão digital do certificado TLS/SSL especificado durante a instalação do Mestre do Scale Out|
|SqlServerName|O nome do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que contém o catálogo SSISDB. Por exemplo, ServerName\\InstanceName.|O nome do SQL Server que é instalada com o Mestre do Scale Out.|
|CleanupCompletedJobsIntervalInMs|O intervalo de limpeza de trabalhos de execução concluídos, em milissegundos.|43200000|
|DealWithExpiredTasksIntervalInMs|O intervalo para lidar com trabalhos de execução expirados, em milissegundos.|300000|
|MasterHeartbeatIntervalInMs|O intervalo de pulsação do Mestre de Expansão, em milissegundos. Essa propriedade especifica o intervalo no qual o Mestre do Scale Out atualiza seu status online no catálogo do SSISDB.|30000|
|SqlConnectionTimeoutInSecs|O tempo de limite de conexão SQL em segundos ao se conectar ao SSISDB.|15|
||||    

## <a name="view-the-scale-out-master-service-log"></a>Exibir o log do serviço do Mestre do Scale Out

O arquivo de log do serviço do Mestre do Scale Out está localizado na pasta `<drive>:\Users\[account]\AppData\Local\SSIS\ScaleOut\Master`. 

O parâmetro *[account]* refere-se à conta que executa o serviço Mestre do Scale Out. Por padrão, essa conta é `SSISScaleOutMaster140`.

## <a name="next-steps"></a>Próximas etapas

[Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)
