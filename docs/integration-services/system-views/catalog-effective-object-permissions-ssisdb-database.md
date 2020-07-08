---
title: catalog.effective_object_permissions (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.effective_object_permissions views [Integration Services]
- effective_object_permissions view [Integration Services]
ms.assetid: e70c4ce9-79f5-44df-ac75-6c29b6e38776
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f47b58cbac71800715a5f2ec091b6ce026484e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673446"
---
# <a name="catalogeffective_object_permissions-ssisdb-database"></a>catalog.effective_object_permissions (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe as permissões efetivas da entidade de segurança atual para todos os objetos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|O tipo de objeto protegível. Os tipos de objetos protegíveis incluem pasta (`1`), projeto (`2`), ambiente (`3`) e operação (`4`).|  
|object_id|**bigint**|O ID (identificador exclusivo) ou a chave primária do objeto.|  
|permission_type|**smallint**|O tipo de permissão.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra os tipos de permissão listados na seguinte tabela:  
  
|Valor de permission_type|Nome da permissão|Descrição da permissão|Tipos de objeto aplicáveis|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Permite que a entidade de segurança leia informações consideradas parte do objeto, como as propriedades. Não permite que a entidade de segurança enumere ou leia o conteúdo de outros objetos contidos no objeto.|Pasta, projeto, ambiente, operação|  
|`2`|MODIFY|Permite que a entidade de segurança modifique informações consideradas parte do objeto, como as propriedades. Não permite que a entidade de segurança modifique outros objetos contidos no objeto.|Pasta, projeto, ambiente, operação|  
|`3`|Execute|Permite que a entidade de segurança execute todos os pacotes no projeto.|Project|  
|`4`|MANAGE_PERMISSIONS|Permite que a entidade de segurança atribua permissões a objetos.|Pasta, projeto, ambiente, operação|  
|`100`|CREATE_OBJECTS|Permite que a entidade de segurança crie objetos na pasta.|Pasta|  
|`101`|READ_OBJECTS|Permite que a entidade de segurança leia todos os objetos na pasta.|Pasta|  
|`102`|MODIFY_OBJECTS|Permite que a entidade de segurança modifique todos os objetos na pasta.|Pasta|  
|`103`|EXECUTE_OBJECTS|Permite que a entidade de segurança execute todos os pacotes de todos os projetos na pasta.|Pasta|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Permite que a entidade de segurança gerencie permissões em todos os objetos na pasta.|Pasta|  
  
 São avaliados apenas os objetos nos quais o chamador tem permissões. As permissões são computadas com base no seguinte:  
  
-   Permissões explícitas  
  
-   Permissões herdadas  
  
-   Associação da entidade de segurança em funções  
  
-   Associação da entidade de segurança em grupos  
  
## <a name="permissions"></a>Permissões  
 Os usuários só podem consultar permissões efetivas para si mesmos e para funções das quais sejam membros.  
  
  
