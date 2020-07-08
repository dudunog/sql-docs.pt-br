---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 79ef41fb52aa431325578195111ee9e4f451d9cf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673009"
---
# <a name="catalogexecutable_statistics"></a>catalog.executable_statistics 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe uma linha para cada executável que é executado, inclusive cada iteração de um executável.  
  
 Um executável é uma tarefa ou um contêiner que você adiciona ao fluxo de controle de um pacote.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|Statistics_id|BIGINT|A ID exclusiva dos dados.|  
|Execution_id|BIGINT|ID exclusiva da instância da execução.<br /><br /> A exibição catalog.executions fornece informações adicionais sobre execuções. Para obter mais informações, consulte [catalog.executions &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).|  
|Executable_id|BIGINT|ID exclusiva do componente do pacote.<br /><br /> A exibição catalog.executables fornece informações adicionais sobre executáveis. Para obter mais informações, consulte [catalog.executables](../../integration-services/system-views/catalog-executables.md).|  
|Execution_path|nvarchar(max)|O caminho de execução completo do componente de pacote, incluindo cada iteração do componente.|  
|Start_time|datetimeoffset(7)|A hora em que o executável entra na fase pré-execução.|  
|End_time|datetimeoffset(7)|A hora em que o executável entra na fase pós-execução.|  
|Execution_duration|INT|O período de tempo que o executável gastou na execução. O valor está em milissegundos.|  
|Execution_result|SMALLINT|O valores possíveis são os seguintes:<br /><br /> 0 (Êxito)<br /><br /> 1 (Falha)<br /><br /> 2 (Conclusão)<br /><br /> 3 (Cancelado)|  
|Execution_value|sql_variant|O valor retornado pela execução. Esse é um valor definido pelo usuário.|  
  
## <a name="permissions"></a>Permissões  
 A exibição exige uma das seguintes permissões:  
  
-   Permissão READ na instância da execução.  
  
-   Associação à função de banco de dados **ssis_admin**.  
  
-   Associação à função de servidor **sysadmin**.  
  
  
