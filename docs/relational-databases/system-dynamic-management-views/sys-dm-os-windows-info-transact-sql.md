---
description: sys.dm_os_windows_info (Transact-SQL)
title: sys.dm_os_windows_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 111e5b732dae02a5bc2bc8dcffebb3b563206f9c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094016"
---
# <a name="sysdm_os_windows_info-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha que exibe informações de versão de sistema operacional Windows.  
  
  Aplica-se somente a SQL Server em execução no Windows. Para ver as informações semelhantes para SQL Server em execução em um host não Windows, como o Linux, use [sys.dm_os_host_info &#40;&#41;do Transact-SQL ](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Para o Windows, retorna o número de versão. Para obter uma lista de valores e descrições, consulte [versão do sistema operacional (Windows)](/windows/desktop/SysInfo/operating-system-version). Não pode ser NULL.|  
|**windows_service_pack_level**|**nvarchar(256)**| Para o Windows, retorna o número de service pack. Não pode ser NULL. |  
|**windows_sku**|**int**|Para o Windows, retorna a ID da SKU (unidade de manutenção de estoque) do Windows. Para obter uma lista de IDs e descrições de SKU, consulte a [função GetProductInfo](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getproductinfo). Permite valor nulo. |  
|**os_language_version**|**int**| Para o Windows, retorna o LCID (identificador de localidade do Windows) do sistema operacional. Para obter uma lista de valores e descrições de LCID, consulte [IDs de localidade atribuídas pela Microsoft](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c). Não pode ser NULL.|  
  
  
## <a name="permissions"></a>Permissões  
A permissão SELECT em sys.dm_os_windows_info é concedida à função Public por padrão. Se revogado, requer a permissão VIEW SERVER STATE no servidor.  

## <a name="limitations-and-restrictions"></a>Limitações e Restrições
Para ver o informatation para SQL em execução em um host não Windows, como o Linux, use [sys.dm_os_host_info &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as colunas da exibição **Sys.dm_os_windows_info** .  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
