---
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65b3853db8fb20ef3c2a21846db59ce0981485cb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85672788"
---
# <a name="catalogexecution_data_statistics"></a>catalog.execution_data_statistics 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream para determinada execução do pacote. As informações desta exibição podem ser usadas para computar a taxa de transferência de dados para um componente.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|A ID (identificador exclusivo) dos dados.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|package_name|**nvarchar(260)**|O nome do primeiro pacote que foi iniciado durante a execução.|  
|task_name|**nvarchar(4000)**|O nome da tarefa de fluxo de dados.|  
|dataflow_path_id_string|**nvarchar(4000)**|A cadeia de caracteres de identificação do caminho de fluxo de dados.|  
|dataflow_path_name|**nvarchar(4000)**|Nome do caminho de fluxo de dados.|  
|source_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que enviou os dados.|  
|destination_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que recebeu os dados.|  
|rows_sent|**bigint**|O número de linhas enviadas ao componentes de origem.|  
|created_time|**datatimeoffset(7)**|A hora em que os valores foram obtidos.|  
|execution_path|**nvarchar(max)**|O caminho de execução do componente.|  
  
## <a name="remarks"></a>Comentários  
  
-   Quando houver várias saídas do componente, uma linha será adicionada para cada uma das saídas.  
  
-   Por padrão, quando uma execução é iniciada, as informações sobre o número de linhas que são enviadas não são registradas em log.  
  
-   Para exibir esses dados para uma execução específica de pacote, defina o nível de log como **Detalhado**. Para saber mais, veja [Habilitar o log para a execução do pacote no servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
