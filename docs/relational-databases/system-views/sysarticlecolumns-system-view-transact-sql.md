---
description: sysarticlecolumns (exibição de sistema) (Transact-SQL)
title: sysarticlecolumns (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a6e359aa7f6c0e7efc4090152b152ab1bfb6fbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460254"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (exibição de sistema) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição **sysarticlecolumns** expõe informações adicionais sobre colunas em artigos publicados. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**int**|Identifica uma coluna em um artigo.|  
|**is_udt**|**int**|Indica se a coluna é uma coluna UDT (User-Defined Data Type). Um valor de **1** indica uma coluna UDT.|  
|**is_xml**|**int**|É se a coluna for uma coluna **XML** . Um valor de **1** indica uma coluna **XML** .|  
|**is_max**|**int**|É se a coluna for uma coluna de tipo de dados de valor grande (**varchar (max)**, **nvarchar (max)** ou **varbinary (max)**). Um valor de **1** indica uma coluna de valor grande.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_articlecolumn ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [&#41;sysarticlecolumns &#40;Transact-SQL ](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
