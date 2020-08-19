---
description: catalog.operations (Banco de Dados SSISDB)
title: catalog.operations (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- operations view [Integration Services]
- catalog.operations view [Integration Services]
ms.assetid: 9455c5b1-60ff-45fc-8599-cc3abbd6daf5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 231fa098ababe70c8a375e3f3f357bcbe90d6f09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422010"
---
# <a name="catalogoperations-ssisdb-database"></a>catalog.operations (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe os detalhes de todas as operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|operation_id|**bigint**|O ID (identificador exclusivo) da operação.|  
|operation_type|**smallint**|O tipo de operação.|  
|created_time|**datetimeoffset**|A hora em que a operação foi criada.|  
|object_type|**smallint**|O tipo de objeto afetado pela operação. O objeto pode ser uma pasta (`10`), um projeto (`20`), um pacote (`30`), um ambiente (`40`) ou uma instância de execução (`50`).|  
|object_id|**bigint**|A ID do objeto afetado pela operação.|  
|object_name|**nvarchar(260)**|O nome do objeto.|  
|status|**int**|O status da operação. Os possíveis valores são criado (`1`), em execução (`2`), cancelado (`3`), com falha (`4`), pendente (`5`), encerrado inesperadamente (`6`), êxito (`7`), parando (`8`) e concluído (`9`).|  
|start_time|**datetimeoffset**|A hora de início da operação.|  
|end_time|**datetimeoffsset**|A hora em que a operação foi concluída.|  
|caller_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário se a Autenticação do Windows tiver sido usada para fazer logon.|  
|caller_name|**nvarchar(128)**|O nome da conta que executou a operação.|  
|process_id|**int**|A ID de processo do processo externo, se aplicável.|  
|stopped_by_sid|**varbinary(85)**|O SID do usuário que interrompeu a operação.|  
|stopped_by_name|**nvarchar(128)**|O nome do usuário que interrompeu a operação.|  
|server_name|**nvarchar(128)**|As informações do servidor e da instância do Windows de uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar(128)**|O nome do computador no qual a instância de servidor está sendo executada.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição mostra uma linha para cada operação no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Permite que o administrador enumere todas as operações lógicas que foram executadas no servidor, como implantar um projeto ou executar um pacote.  
  
 Essa exibição mostra os seguintes tipos de operação, conforme listado na coluna **operation_type**:  
  
|Valor de **operation_type**|Descrição de **operation_type**|Descrição de **object_id**|Descrição de **object_name**|  
|-------------------------------|-------------------------------------|--------------------------------|----------------------------------|  
|`1`|Inicialização [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|**NULL**|**NULL**|  
|`2`|Janela de retenção<br /><br /> (trabalho do SQL Agent)|**NULL**|**NULL**|  
|`3`|MaxProjectVersion<br /><br /> (trabalho do SQL Agent)|**NULL**|**NULL**|  
|`101`|**deploy_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`106`|**restore_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`200`|**create_execution** e **start_execution**<br /><br /> (Procedimentos armazenados)|Project ID|**NULL**|  
|`202`|**stop_operation**<br /><br /> (Procedimento armazenado)|Project ID|**NULL**|  
|`300`|**validate_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`301`|**validate_package**<br /><br /> (Procedimento armazenado)|Project ID|Nome do pacote|  
|`1000`|**configure_catalog**<br /><br /> (Procedimento armazenado)|**NULL**|**NULL**||  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
