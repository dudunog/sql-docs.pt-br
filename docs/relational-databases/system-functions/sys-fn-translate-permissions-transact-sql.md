---
description: sys.fn_translate_permissions (Transact-SQL)
title: sys. fn_translate_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
author: rothja
ms.author: jroth
ms.openlocfilehash: 1069d5b76d6ee404ddd2e671eb6a7b63396424ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481757"
---
# <a name="sysfn_translate_permissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Traduz o bitmask de permissões retornado pelo Rastreamento do SQL em uma tabela de nomes de permissões.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geral*  
 É o tipo de protegível ao qual a permissão é aplicada. o *nível* é **nvarchar (60)**.  
  
 *perms*  
 É um bitmask retornado na coluna de permissões. *perms* é **varbinary (16)**.  
  
## <a name="returns"></a>Retornos  
 **table**  
  
## <a name="remarks"></a>Comentários  
 O valor retornado na coluna **permissões** de um rastreamento do SQL é uma representação de inteiro de um bitmask usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular as permissões efetivas. Cada um dos 25 tipos de protegíveis tem seu próprio conjunto de permissões com valores numéricos correspondentes. **Sys. fn_translate_permissions** converte esse bitmask em uma tabela de nomes de permissões.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir usa `sys.fn_builtin_permissions` para exibir as permissões que se aplicam a certificados e, em seguida, usa `sys.fn_translate_permissions` para retornar os resultados do bitmask de permissões.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
