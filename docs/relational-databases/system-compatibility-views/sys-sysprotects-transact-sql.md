---
description: sys.sysprotects (Transact-SQL)
title: sys.sysprotege (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprotects
- sys.sysprotects_TSQL
- sys.sysprotects
- sysprotects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprotects compatibility view
- sysprotects system table
ms.assetid: 49c9658d-fb51-4c77-94a0-fba699b0102d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 417ef61ac045151c4ea2399d1192fdbff0519736
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095366"
---
# <a name="syssysprotects-transact-sql"></a>sys.sysprotects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre permissões que foram aplicadas a contas de segurança no banco de dados por meio das instruções GRANT e DENY.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do objeto ao qual se aplicam as permissões.|  
|**UID**|**smallint**|ID do usuário ou grupo ao qual se aplicam as permissões. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**action**|**tinyint**|Pode ter uma das seguintes permissões:<br /><br /> 26 = REFERENCES<br /><br /> 178 = CREATE FUNCTION<br /><br /> 193 = SELECT<br /><br /> 195 = INSERIR<br /><br /> 196 = EXCLUIR<br /><br /> 197 = ATUALIZAÇÃO<br /><br /> 198 = CREATE TABLE<br /><br /> 203 = CREATE DATABASE<br /><br /> 207 = CREATE VIEW<br /><br /> 222 = CREATE PROCEDURE<br /><br /> 224 = EXECUTE<br /><br /> 228 = BACKUP DATABASE<br /><br /> 233 = CREATE DEFAULT<br /><br /> 235 = BACKUP LOG<br /><br /> 236 = CREATE RULE|  
|**protecttype**|**tinyint**|Pode ter os seguintes valores:<br /><br /> 204 = GRANT_W_GRANT<br /><br /> 205 = GRANT<br /><br /> 206 = DENY|  
|**colunas**|**varbinary(8000)**|Bitmap de colunas aos quais se aplicam as permissões SELECT ou UPDATE.<br /><br /> Bit 0 = Todas as colunas.<br /><br /> Bit 1 = As permissões se aplicam a essa coluna.<br /><br /> NULL = Sem-informações.|  
|**cesso**|**smallint**|ID do usuário que emitiu as permissões GRANT ou DENY. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
