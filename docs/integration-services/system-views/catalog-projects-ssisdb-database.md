---
title: catalog.projects (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 408cbc5749487efaa25ef5d8acd42d346fc9df6e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85671440"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe os detalhes de todos os projetos exibidos no catálogo do **SSISDB**.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|O identificador exclusivo (ID) do projeto.|  
|folder_id|**bigint**|O ID exclusivo da pasta onde o projeto reside.|  
|name|**sysname**|O nome do projeto.|  
|descrição|**nvarchar(1024)**|A descrição opcional do projeto.|  
|project_format_version|**int**|A versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para desenvolver o projeto.|  
|deployed_by_sid|**varbinary(85)**|O identificador de segurança (SID) exclusivo do usuário que instalou o projeto.|  
|deployed_by_name|**nvarchar(128)**|O nome do usuário que instalou o projeto.|  
|last_deployed_time|**datetimeoffset(7)**|A data e a hora em que o projeto foi implantado ou reimplantado.|  
|created_time|**datetimeoffset(7)**|A data e hora em que o projeto foi criado.|  
|object_version_lsn|**bigint**|A versão do projeto. Não há garantia de que este número seja sequencial.|  
|validation_status|**char(1)**|O status da validação.|  
|last_validation_time|**datetimeoffset(7)**|A hora da última validação.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada projeto no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**.  
  
> [!NOTE]  
>  Se você tiver a permissão READ em um projeto, também terá a permissão READ em todas as referências de pacotes e ambientes associadas ao projeto. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
