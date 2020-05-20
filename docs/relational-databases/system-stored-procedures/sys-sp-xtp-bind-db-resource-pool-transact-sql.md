---
title: sys. sp_xtp_bind_db_resource_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_bind_db_resource_pool_TSQL
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool_TSQL
- sys.sp_xtp_bind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool
ms.assetid: c2a78073-626b-4159-996e-1808f6bfb6d2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dfdfbe678e5b91d72e19a0300f9f1feec77c9d75
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814491"
---
# <a name="syssp_xtp_bind_db_resource_pool-transact-sql"></a>sys.sp_xtp_bind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Associa o banco de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] especificado para o pool de recursos especificado. O banco de dados e o pool de recursos devem existir antes de executar o `sys.sp_xtp_bind_db_resource_pool`.  
  
 Este procedimento do sistema cria uma associação entre o pool do Administrador de Recursos identificado pelo resource_pool_name e o banco de dados identificado por database_name Não é necessário que o banco de dados tenha todos os objetos com otimização de memória no momento da associação. Na ausência de objetos com otimização de memória, nenhuma memória é obtida do pool de recursos. Esta associação será usada pelo Administrador de Recursos para gerenciar a memória alocada por alocadores do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] conforme descrito abaixo.  
  
 Se já houver uma associação no local para um determinado banco de dados, o procedimento retornará um erro.  Em nenhuma hipótese um banco de dados pode ter mais de uma associação ativa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sys.sp_xtp_bind_db_resource_pool 'database_name', 'resource_pool_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 database_name  
 O nome de um banco de dados habilitado para [!INCLUDE[hek_2](../../includes/hek-2-md.md)] existente.  
  
 resource_pool_name  
 O nome de um pool de recursos existente.  
  
## <a name="messages"></a>Mensagens  
 Quando um erro ocorrer, o `sp_xtp_bind_db_resource_pool` retornará uma dessas mensagens.  
  
 **O banco de dados não existe**  
 Database_name deve se referir a um banco de dados existente. Se não houver nenhum banco de dados com a ID especificada, a mensagem a seguir será retornada:   
*A ID de banco de dados% d não existe.  Use uma ID de banco de dados válida para esta associação.*  
  
```  
Msg 911, Level 16, State 18, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB213' does not exist. Make sure that the name is entered correctly.  
```  
  
**Este é um banco de dados do sistema**  
 As tabelas do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] não podem ser criadas em bancos de dados do sistema.  Portanto, isso é inválido para criar uma associação de memória do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] para esse banco de dados.  O seguinte erro é retornado.  
*Database_name% s se refere a um banco de dados do sistema.  Os pools de recursos só podem ser associados a um banco de dados de usuário.*  
  
```  
Msg 41371, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Binding to a resource pool is not supported for system database 'master'. This operation can only be performed on a user database.  
```  
  
**O pool de recursos não existe**  
 O pool de recursos identificado pelo resource_pool_name deve existir antes de executar o `sp_xtp_bind_db_resource_pool`.  Se não houver nenhum pool com a ID especificada, o erro a seguir será retornado:  
*O pool de recursos% s não existe.  Insira um nome de pool de recursos válido.*  
  
```  
Msg 41370, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Resource pool 'Pool_Hekaton' does not exist or resource governor has not been reconfigured.  
```  
  
**Pool_name refere-se a um pool do sistema reservado**  
 Os nomes de pool "interno" e "padrão" são reservados para pools do sistema.  Não é válido associar explicitamente um banco de dados a nenhum deles.  Se um nome do pool do sistema é inserido, o erro a seguir será retornado:  
*O pool de recursos% s é um pool de recursos do sistema.  Os pools de recursos do sistema não podem ser explicitamente associados a um banco de dados usando este procedimento.*  
  
```  
Msg 41373, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB' cannot be explicitly bound to the resource pool 'internal'. A database can only be bound only to a user resource pool.  
```  
  
**O banco de dados já está associado a outro pool de recursos**  
 Um banco de dados pode estar associado a apenas um pool de recursos de cada vez. As associações de banco de dados a pools de recursos devem ser explicitamente removidas antes de serem associadas a outro pool. Consulte [Sys. sp_xtp_unbind_db_resource_pool &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md).  
*O banco de dados% s já está associado ao pool de recursos% s.  Você deve desassociar antes de poder criar uma nova associação.*  
  
```  
Msg 41372, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 54  
Database 'Hekaton_DB' is currently bound to a resource pool. A database must be unbound before creating a new binding.  
```  
  
 Quando obtém êxito, o `sp_xtp_bind_db_resource_pool` retorna a seguinte mensagem.  
  
**Associação com êxito**  
 Quando há êxito, a função retorna a seguinte mensagem de êxito, que é registrada no SQL ERRORLOG  
*Uma associação de recursos foi criada com êxito entre o banco de dados com ID %d e o pool de recursos com ID %d.*  
  
## <a name="examples"></a>Exemplos  
a.  O código de exemplo a seguir associa um banco de dados Hekaton_DB ao pool de recursos Pool_Hekaton.  
  
```sql  
sys.sp_xtp_bind_db_resource_pool N'Hekaton_DB', N'Pool_Hekaton'  
```  
 
 A associação entra em vigor da próxima vez que o banco de dados é colocado online.  
 
 B. Exemplo expandido de exemplo acima, que inclui algumas verificações básicas.  Execute o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] em[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]\:
 
```sql
DECLARE @resourcePool sysname = N'Pool_Hekaton';
DECLARE @database sysname = N'Hekaton_DB';

-- Check whether resource pool exists
IF NOT EXISTS (
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = @resourcePool
    )
BEGIN
    SELECT N'Resource pool "' + @resourcePool + N'" does not exist or resource governor has not been reconfigured.';
END
-- Check whether database is already bound to a resource pool
ELSE IF EXISTS (
    SELECT p.name
    FROM sys.databases d
    JOIN sys.resource_governor_resource_pools p
    ON d.resource_pool_id = p.pool_id
    WHERE d.name = @database
    )
BEGIN
    SELECT N'Database "' + @database + N'" is currently bound to resource pool "' + @resourcePool  + N'". A database must be unbound before creating a new binding.';
END
-- Bind resource pool to database.
ELSE BEGIN
    EXEC sp_xtp_bind_db_resource_pool @database, @resourcePool; 
END 
``` 
  
## <a name="requirements"></a>Requisitos  
  
-   O banco de dados especificado por `database_name` e o pool de recursos especificado por `resource_pool_name` devem existir antes de associá-los.  
  
-   Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte Também  
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
