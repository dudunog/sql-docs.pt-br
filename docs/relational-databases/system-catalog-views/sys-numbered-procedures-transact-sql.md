---
description: sys.numbered_procedures (Transact-SQL)
title: sys.numbered_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 34d67487512792261397d80e9353edecf4775b82
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095486"
---
# <a name="sysnumbered_procedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contém uma linha para cada procedimento armazenado do SQL Server que foi criado como um procedimento numerado. Isto não mostra uma linha para o procedimento armazenado básico (número = 1). As entradas para os procedimentos armazenados base podem ser encontradas em exibições como **Sys. Objects** e **Sys. procedures**.  
  
> [!IMPORTANT]  
>  Os procedimentos numerados são preteridos. O uso de procedimentos numerados é desaconselhável. Um evento DEPRECATION_ANNOUNCEMENT será acionado quando uma consulta que usa essa exibição do catálogo for compilada.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto do procedimento armazenado.|  
|**procedure_number**|**smallint**|Número deste procedimento no objeto, 2 ou maior.|  
|**defini**|**nvarchar(max)**|O texto do SQL Server que define este procedimento.<br /><br /> NULL = criptografado.|  
  
> [!NOTE]  
>  Não há suporte para os parâmetros XML e CLR em procedimentos numerados.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
