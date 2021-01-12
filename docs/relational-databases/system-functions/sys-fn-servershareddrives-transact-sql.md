---
description: sys.fn_servershareddrives (Transact-SQL)
title: sys.fn_servershareddrives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_servershareddrives
- fn_servershareddrives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_servershareddrives function
- shared drives [SQL Server]
- names [SQL Server], shared drives
- sys.fn_serversharedrives function
ms.assetid: ff01eff7-8cb6-460c-ba7a-6a52bda6d471
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f8260d8c84276239864d6d3d7639766b8a62b5f3
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096366"
---
# <a name="sysfn_servershareddrives-transact-sql"></a>sys.fn_servershareddrives (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna os nomes das unidades compartilhadas usadas pelo servidor clusterizado.  
  
> [!IMPORTANT]  
>  Essa função de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é incluída para fins de compatibilidade com versões anteriores. É recomendável usar [sys.dm_io_cluster_valid_path_names &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_servershareddrives()  
```  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Se o servidor atual for um servidor clusterizado, **fn_servershareddrives** retornará o nome da unidade das unidades compartilhadas.  
  
 Se a instância do servidor atual não for um servidor clusterizado, **fn_servershareddrives** retornará um conjunto de linhas vazio.  
  
## <a name="remarks"></a>Comentários  
 `fn_servershareddrives` retorna uma lista de unidades compartilhadas usada por esse servidor clusterizado. Essas unidades compartilhadas pertencem ao mesmo grupo de clusters que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recurso. Além disso, o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende dessas unidades.  
  
 Esta função é útil para identificar as unidades disponíveis aos usuários.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão VIEW SERVER STATE para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte usa `fn_servershareddrives` para consultar em uma instância de servidor clusterizado:  
  
```  
SELECT * FROM fn_servershareddrives();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 DriveName  
  
 -------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.dm_io_cluster_valid_path_names ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_io_cluster_shared_drives ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)  
  
  
