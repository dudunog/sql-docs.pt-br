---
description: sysssislog (Transact-SQL)
title: sysssislog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9aef51cb3297cd83b68fa42c71dcd993fb418830
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473091"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada entrada de log gerada por pacotes ou as tarefas e contêineres em tempo de execução. Essa tabela é criada no banco de dados msdb quando você instala o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se você configurar o registro em log para registrar em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente, uma tabela sysssislog com esse formato será criada no banco de dados especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] grava entradas de log nesta tabela **somente** quando os pacotes usam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de log.  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|O identificador exclusivo da entrada do log.|  
|event|**sysname**|O nome do evento que gerou a entrada do log.|  
|computer|**nvarchar**|O computador no qual o pacote foi executado quando a entrada do log foi gerada.|  
|operador|**nvarchar**|O nome de usuário da pessoa que executou o pacote que gerou a entrada do log.|  
|source|**nvarchar**|O nome do executável, no pacote, que gerou a entrada do log.|  
|sourceid|**uniqueidentifier**|O GUID do executável, no pacote, que gerou a entrada do log.|  
|executionid|**uniqueidentifier**|A GUID da instância de execução do executável que gerou a entrada do log.|  
|starttime|**datetime**|A hora em que o pacote começou a ser executado.|  
|endtime|**datetime**|A hora em que o pacote foi concluído.<br /><br /> Este recurso não está implementado. O valor na coluna endtime sempre é igual ao valor na coluna starttime.|  
|datacode|**int**|Um valor inteiro opcional que geralmente indica o resultado da execução do contêiner ou da tarefa.|  
|databytes|**imagem**|Uma matriz de byte opcional que contém informações adicionais.|  
|mensagem|**nvarchar**|Uma descrição do evento e as informações associadas a ele.|  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
