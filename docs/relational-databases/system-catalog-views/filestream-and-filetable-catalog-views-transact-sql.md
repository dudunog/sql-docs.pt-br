---
description: Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)
title: Exibições de catálogo FileStream e Filetable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c50e3042b82540e17ec6be721d84ba9cfe469c87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482231"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta seção descreve as exibições de catálogo relacionadas ao recurso FileTable.  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Exibições de catálogo FileStream e filetable (Transact-SQL)
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 Exibe informações sobre o nível de acesso não transacional a dados FILESTREAM em FileTables que estão habilitadas. Contém uma linha para cada banco de dados na instância do SQL Server.  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 Exibe uma lista dos objetos definidos pelo sistema que são relacionados a FileTables. Contém uma linha para cada objeto definido pelo sistema.  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 Retorna uma linha para cada FileTable. Herda de **Sys. Tables**.  

## <a name="see-also"></a>Consulte Também
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Procedimentos armazenados de fluxo de arquivos e FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
