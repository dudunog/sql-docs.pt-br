---
title: sys. dm_filestream_file_io_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_filestream_file_io_handles
- sys.dm_filestream_file_io_handles
- dm_filestream_file_io_handles_TSQL
- sys.dm_filestream_file_io_handles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_handle catalog view
ms.assetid: e59632f4-3292-419f-9217-ca375749f1a5
author: stevestein
ms.author: sstein
ms.openlocfilehash: a96bcedaa3922ebb0691ac949f9eb15ed28336b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103306"
---
# <a name="sysdm_filestream_file_io_handles-transact-sql"></a>sys.dm_filestream_file_io_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe os identificadores de arquivos que o NSO (proprietário do namespace) conhece. Os identificadores FileStream que um cliente obteve usando **OpenSqlFilestream** são exibidos por essa exibição.  
  
|Coluna|Type|Descrição|  
|------------|----------|-----------------|  
|**handle_context_address**|**varbinary (8)**|Mostra o endereço da estrutura NSO interna associada à alça do cliente. Permite valor nulo.|  
|**creation_request_id**|**int**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Não permite valor nulo.|  
|**creation_irp_id**|**int**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Não permite valor nulo|  
|**handle_id**|**int**|Mostra a ID exclusiva deste identificador que é atribuída pelo driver. Não permite valor nulo.|  
|**creation_client_thread_id**|**varbinary (8)**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Permite valor nulo.|  
|**creation_client_process_id**|**varbinary (8)**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Permite valor nulo.|  
|**filestream_transaction_id**|**varbinary(128)**|Mostra a ID da transação associada ao identificador específico. Esse é o valor retornado pela função **GET_FILESTREAM_TRANSACTION_CONTEXT** . Use este campo para ingressar na exibição **Sys. dm_filestream_file_io_requests** . Permite valor nulo.|  
|**access_type**|**nvarchar(60)**|Não permite valor nulo.|  
|**logical_path**|**nvarchar(256)**|Mostra o nome de caminho lógico do arquivo que este identificador abriu. Esse é o mesmo nome de caminho que é retornado pelo **. Método PathName** de FileStream **varbinary**(**Max**). Permite valor nulo.|  
|**physical_path**|**nvarchar(256)**|Mostra o nome de caminho NTFS real do arquivo. Esse é o mesmo nome de caminho retornado pelo **. Método PhysicalPathName** do FileStream **varbinary**(**Max**). Ele é habilitado pelo sinalizador de rastreamento 5556. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de FileStream e Filetable &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
