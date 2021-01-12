---
description: sys.dm_server_memory_dumps (Transact-SQL)
title: sys.dm_server_memory_dumps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 29ae5e940daffd0487d5d3e4514b5b624dd1320e
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096484"
---
# <a name="sysdm_server_memory_dumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada arquivo de despejo de memória gerado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Use essa exibição de gerenciamento dinâmico para solucionar problemas potenciais.  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**nome do arquivo**|**nvarchar(256)**|Caminho e nome do arquivo de despejo de memória. Não pode ser nulo.|  
|**creation_time**|**datetimeoffset(7)**|Data e hora em que o arquivo foi criado. Não pode ser nulo.|  
|**size_in_bytes**|**bigint**|Tamanho (em bytes) do arquivo. Permite valor nulo.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 O tipo de despejo pode ser um minidespejo, despejo de todos os threads ou um despejo completo. Os arquivos têm uma extensão .mdmp.  
  
## <a name="security"></a>Segurança  
 Os arquivos de despejo podem conter informações confidenciais. Para ajudar a proteger essas informações, você pode usar uma lista de controle de acesso (ACL) para restringir o acesso aos arquivos ou copiar os arquivos para uma pasta que tenha acesso restrito. Por exemplo, antes de enviar seus arquivos de depuração para os serviços de suporte da Microsoft, recomendamos que você remova informações confidenciais ou confidenciais.  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
  
