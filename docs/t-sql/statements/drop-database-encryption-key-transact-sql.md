---
description: DROP DATABASE ENCRYPTION KEY (Transact-SQL)
title: DROP DATABASE ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP DATABASE ENCRYPTION KEY
- DROP_DATABASE_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key, drop
- DROP DATABASE ENCRYPTION KEY statement
ms.assetid: 9231bd89-75e1-45c4-b4c8-13f08695af68
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ee76d78af88b8831db9db44489d6fcf5caa74e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496791"
---
# <a name="drop-database-encryption-key-transact-sql"></a>DROP DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Descarta uma chave de criptografia de banco de dados usada em criptografia de banco de dados transparente. Para obter mais informações sobre criptografia de banco de dados transparente, consulte [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
> [!IMPORTANT]  
>  O backup do certificado que estava protegendo a chave de criptografia de banco de dados deverá ser mantido até mesmo se a criptografia não estiver mais habilitada em um banco de dados. Mesmo que o banco de dados não esteja mais criptografado, partes do log de transações ainda poderão permanecer protegidas e talvez o certificado seja necessário para algumas operações até a realização do backup completo do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP DATABASE ENCRYPTION KEY  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
 Se o banco de dados for criptografado, você deverá primeiro remover a criptografia do banco de dados usando a instrução ALTER DATABASE. Aguarde a conclusão da descriptografia antes de remover a chave de criptografia de banco de dados. Para obter mais informações sobre a instrução ALTER DATABASE, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para exibir o estado do banco de dados, use a exibição de gerenciamento dinâmico [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a criptografia do banco de dados e descarta a chave de criptografia do banco de dados.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION OFF;  
GO  
/* Wait for decryption operation to complete, look for a   
value of  1 in the query below. */  
SELECT encryption_state  
FROM sys.dm_database_encryption_keys;  
GO  
USE AdventureWorks2012;  
GO  
DROP DATABASE ENCRYPTION KEY;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir remove a criptografia TDE e então remove a chave de criptografia do banco de dados.  
  
```  
ALTER DATABASE AdventureWorksPDW2012  
    SET ENCRYPTION OFF;  
GO  
/* Wait for decryption operation to complete, look for a   
value of  1 in the query below. */  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;   
GO  
USE AdventureWorksPDW2012;  
GO  
DROP DATABASE ENCRYPTION KEY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
  
  

