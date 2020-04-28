---
title: sys. filetable_system_defined_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd05f24ab90844065b708230ee016ce9ce78bfbd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005153"
---
# <a name="sysfiletable_system_defined_objects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe uma lista dos objetos definidos pelo sistema que são relacionados a FileTables. Contém uma linha para cada objeto definido pelo sistema.  
  
 Quando você cria uma FileTable, objetos relacionados, como restrições e índices, são criados ao mesmo tempo. Você não pode alterar ou remover esses objetos. Eles desaparecem apenas quando a própria FileTable é removida.  
  
 Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto definido pelo sistema relacionado a uma FileTable.<br /><br /> Faz referência ao objeto em **Sys. Objects**.|  
|**parent_object_id**|**int**|ID do objeto da FileTable pai.<br /><br /> Faz referência ao objeto em **Sys. Objects**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, alterar e remover filetables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
