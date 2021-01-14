---
description: sys.dm_exec_valid_use_hints (Transact-SQL)
title: sys.dm_exec_valid_use_hints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: de99c9372846525349df3f9f312222e322bfe751
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98171388"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys.dm_exec_valid_use_hints (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

Retorna nomes de dicas de [dica de uso](../../t-sql/queries/hints-transact-sql-query.md#use_hint) com suporte. Ele lista um nome de dica por linha.  
  
Use essa DMV para ver a lista de todas as dicas com suporte na notação de dica de uso.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**sysname**|O nome da dica.|

Consulte [dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md#use_hint) para obter descrições de cada dica.

Introduzido no [!INCLUDE[ssSQL15_md](../../includes/sssql16-md.md)] SP1.
  
## <a name="see-also"></a>Consulte Também  
    
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

