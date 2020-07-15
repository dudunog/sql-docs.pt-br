---
title: Hierarquia de permissões (Mecanismo de Banco de Dados) | Microsoft Docs
description: Saiba mais sobre a hierarquia de entidades que podem ser protegidas com permissões, conhecidas como protegíveis, no Mecanismo de Banco de Dados do SQL Server.
ms.custom: ''
ms.date: 03/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a32748e7714bebef62a67f7a3e7d5fb9f8babd36
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009385"
---
# <a name="permissions-hierarchy-database-engine"></a>Hierarquia de permissões (Mecanismo de Banco de Dados)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerencia uma coleção hierárquica de entidades que podem ser protegidas com permissões. Essas entidades são conhecidas como *protegíveis*. Os protegíveis mais proeminentes são servidores e bancos de dados, mas podem ser definidas permissões discretas em um nível muito mais específico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regula as ações de entidades de segurança em protegíveis verificando se as permissões apropriadas foram concedidas.  
  
 A ilustração a seguir mostra todas as relações entre as hierarquias de permissões do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 O sistema de permissões funciona da mesma em todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssDW](../../includes/ssdw-md.md)]e [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. No entanto, alguns recursos não estão disponíveis em todas as versões. Por exemplo, a permissão de nível de servidor não pode ser configurada em produtos do Azure.  
  
 ![Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados](../../relational-databases/security/media/wj-security-layers.gif "Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados")  
  
## <a name="chart-of-sql-server-permissions"></a>Gráfico de permissões do SQL Server  
 Para obter um gráfico com tamanho de um cartaz de todas as permissões do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em formato pdf, consulte [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster).  
  
## <a name="working-with-permissions"></a>Trabalhando com permissões  
 As permissões podem ser manipuladas com as conhecidas consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] GRANT, DENY e REVOKE. Informações sobre permissões são visíveis nas exibições de catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) e [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) . Há também suporte para informações de permissões de consulta usando funções internas.  
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
