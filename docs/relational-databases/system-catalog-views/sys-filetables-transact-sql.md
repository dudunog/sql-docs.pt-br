---
description: sys.filetables (Transact-SQL)
title: sys. filetables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7ac470d0cdc64860721f045a3108c0221d20e219
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482142"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada FileTable no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).    
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**||Número de identificação do objeto. É exclusivo em um banco de dados.<br /><br /> Para obter mais informações, [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_enabled**|**bit**|1 = A FileTable está no estado 'habilitado'.|  
|**directory_name**|**varchar(255)**|Nome do diretório raiz de uma FileTable.|  
|**filename_collation_id**||É o identificador de ordenação definido para o FileTable|  
|**filename_collation_name**||É o nome da ordenação definido para o FileTable.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar filetables](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
