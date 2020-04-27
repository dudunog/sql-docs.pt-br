---
title: sys. routes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bfdd322107da1a08edb3933aee9d5b79b6c2b47a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904431"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por rota. O Service Broker usa rotas para localizar o endereço de rede para um serviço.   

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da rota, exclusivo no banco de dados. Não é NULLABLE.|  
|**route_id**|**int**|Identificador para a rota. Não é NULLABLE.|  
|**principal_id**|**int**|Identificador para o principal de banco de dados que é proprietário da rota. É NULLABLE.|  
|**remote_service_name**|**nvarchar(256)**|Nome do serviço remoto. É NULLABLE.|  
|**broker_instance**|**nvarchar(128)**|Identificador do agente que hospeda o serviço remoto. É NULLABLE.|  
|**existência**|**datetime**|A data e hora em que a rota expira. Observe que esse valor não usa o fuso horário local. Em vez disso, o valor mostra a hora de expiração para UTC. É NULLABLE.|  
|**address**|**nvarchar(256)**|Endereço de rede para o qual o Service Broker envia mensagens ao serviço remoto. É NULLABLE. Para Instância Gerenciada do Banco de Dados SQL, o endereço deve ser local.|  
|**mirror_address**|**nvarchar(256)**|Endereço de rede do parceiro de espelhamento para o servidor especificado no endereço. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
