---
title: DDL com suporte para módulos T-SQL compilados nativamente | Microsoft Docs
description: Saiba mais sobre constructos DDL compatíveis com módulos T-SQL compilados nativamente, como procedimentos armazenados, UDFs escalares, TVFs embutidos e gatilhos.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9c2a91b1568b139038cad32e81e273d564fbec98
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715379"
---
# <a name="supported-ddl-for-natively-compiled-t-sql-modules"></a>DDL com suporte para módulos T-SQL compilados nativamente
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico lista as construções DDL com suporte para módulos T-SQL compilados nativamente, como procedimentos armazenados, UDFs escalares, TVFs embutidos e gatilhos.  
  
 Para obter informações sobre os recursos e a área de superfície do T-SQL que pode ser usada como parte dos módulos compilados de modo nativo do T-SQL, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Para obter informações sobre construções sem suporte, veja [Construções do Transact-SQL sem suporte pelo OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Há suporte para o seguinte:  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
-   [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
-   Instruções [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) e INSERT SELECT  
  
-   SCHEMABINDING e BEGIN ATOMIC (necessário para procedimentos armazenados compilados nativamente)  
  
     Para saber mais, consulte [Creating Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
-   NATIVE_COMPILATION  
  
     Para saber mais, consulte [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md).  
  
-   Parâmetros e variáveis podem ser declarados como NOT NULL (disponível somente para módulos compilados nativamente: procedimentos armazenados compilados nativamente e funções compiladas nativamente, escalares e definidas pelo usuário).  
  
-   Parâmetros com valor de tabela.  
  
     Para obter mais informações, veja [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
-   EXECUTE AS OWNER, SELF, CALLER e usuário.  
  
-   Permissões GRANT e DENY em tabelas e procedimentos.  
  
     Para obter mais informações, veja [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md) e [Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
