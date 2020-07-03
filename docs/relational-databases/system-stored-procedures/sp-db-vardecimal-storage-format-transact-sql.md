---
title: sp_db_vardecimal_storage_format (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6122a9b2720331b8211a06db051492946f4209b4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85867582"
---
# <a name="sp_db_vardecimal_storage_format-transact-sql"></a>sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o formato de armazenamento vardecimal atual de um banco de dados ou habilita um banco de dados para formato de armazenamento vardecimal.  A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], os bancos de dados de usuário ficam sempre habilitados. A habilitação de bancos de dados para o formato de armazenamento vardecimal é necessária apenas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
> [!IMPORTANT]  
>  Alterar o estado do formato de armazenamento vardecimal de um banco de dados pode afetar backup e recuperação, espelhamento de banco de dados, sp_attach_db, envio de logs e replicação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname =] '*database_name*'  
 É o nome do banco de dados para o qual o formato de armazenamento será alterado. *database_name* é **sysname**, sem padrão. Se o nome do banco de dados for omitido, os status do formato de armazenamento vardecimal de todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão retornados.  
  
 [ @vardecimal_storage_format =] {' On ' | ' Desativado '}  
 Especifica se o formato de armazenamento vardecimal está habilitado. @vardecimal_storage_format pode ser ON ou OFF. O parâmetro é **varchar (3)**, sem padrão. Se um nome de banco de dados for fornecido, mas o @vardecimal_storage_format for omitido, a configuração atual do banco de dados especificado será retornada. Esse argumento não tem nenhum efeito no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou em versões posteriores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se o formato de armazenamento do banco de dados não puder ser alterado, sp_db_vardecimal_storage_format retornará um erro. Se o banco de dados já estiver no estado especificado, o procedimento armazenado não terá nenhum efeito.  
  
 Se o @vardecimal_storage_format argumento não for fornecido, retornará o nome do banco de dados de colunas e o estado vardecimal.  
  
## <a name="remarks"></a>Comentários  
 sp_db_vardecimal_storage_format retorna o estado de vardecimal, mas não pode alterar o estado de vardecimal.  
  
 sp_db_vardecimal_storage_format falhará nas seguintes circunstâncias:  
  
-   Há usuários ativos no banco de dados.  
  
-   O banco de dados está habilitado para espelhamento.  
  
-   A edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte ao formato de armazenamento vardecimal.  
  
 Para alterar o formato de armazenamento vardecimal para OFF, um banco de dados deve ser definido como modo de recuperação simples. Quando um banco de dados está definido como modo de recuperação simples, a cadeia de logs é interrompida. Execute um backup completo do banco de dados depois de definir o formato de armazenamento vardecimal como OFF.  
  
 A alteração do estado para OFF falhará se houver tabelas que usam compactação de banco de dados vardecimal. Para alterar o formato de armazenamento de uma tabela, use [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para determinar quais tabelas de um banco de dados usam o formato de armazenamento vardecimal, use a função `OBJECTPROPERTY` e procure a propriedade `TableHasVarDecimalStorageFormat`, conforme mostrado no exemplo a seguir.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>Exemplos  
 O código a seguir habilita a compactação no banco de dados `AdventureWorks2012`, confirma o estado e, em seguida, compacta as colunas decimais e numéricas da tabela `Sales.SalesOrderDetail`.  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
