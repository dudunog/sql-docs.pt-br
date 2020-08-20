---
description: Procedimentos armazenados de fluxo de arquivos e FileTable (Transact-SQL)
title: Procedimentos armazenados do sistema Filetable e FileStream (Transact-SQL) | Microsoft Docs
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4b16bd28de1b6166cfcea3634c02d48ab8bdc400
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489715"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Procedimentos armazenados do sistema Filetable e FileStream (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta seção descreve os procedimentos armazenados do sistema para o recurso Filetable e FileStream.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Procedimentos armazenados do sistema FileStream e Filetable
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   Força a execução do coletor de lixo FILESTREAM, excluindo qualquer arquivo FILESTREAM desnecessário.

  [sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  Fecha identificadores de arquivos não transacionais para dados de FileTable.


## <a name="see-also"></a>Confira também
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
