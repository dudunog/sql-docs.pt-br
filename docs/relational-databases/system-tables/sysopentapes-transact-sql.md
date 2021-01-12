---
description: sysopentapes (Transact-SQL)
title: sysopentapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: cawrites
ms.author: chadam
ms.openlocfilehash: 0cb05c0ac88f7f362651b872fa84598a656ff25d
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096051"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada dispositivo de fita aberto atualmente. Essa exibição é armazenada no banco de dados **mestre** .  
  
> [!IMPORTANT]  
>  Essa tabela do sistema é incluída como uma exibição para compatibilidade com versões anteriores. Em vez disso, use o sys.dm_io_backup_tapes &#40;exibição de gerenciamento dinâmico [&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) .  
  
> [!NOTE]  
>  Não é possível descartar a exibição **sysopentapes** .  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64)**|Nome de arquivo físico do dispositivo de fita aberto. Para obter mais informações sobre como abrir e liberar dispositivos de fita, consulte [BACKUP &#40;Transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) e [restaurar &#40;&#41;do Transact-SQL ](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 O usuário precisa da permissão VIEW SERVER STATE no servidor.  
  
  
