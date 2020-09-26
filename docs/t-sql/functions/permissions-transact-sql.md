---
description: PERMISSIONS (Transact-SQL)
title: PERMISSIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERMISSIONS_TSQL
- PERMISSIONS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- users [SQL Server], permissions status
- checking permission status
- security [SQL Server], permissions
- verifying permission status
- testing permissions
- PERMISSIONS function
ms.assetid: 81625a56-b160-4424-91c5-1ce8b259a8e6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1bbd07982bc45b3fbd32b140f74a9a0f32fa3c3a
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380737"
---
# <a name="permissions-transact-sql"></a>PERMISSIONS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna um valor contendo um bitmap que indica as permissões de instrução, objeto ou coluna do usuário atual.  
  
 **Importante** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) e [Has_Perms_By_Name](../../t-sql/functions/has-perms-by-name-transact-sql.md) em vez disso. O uso contínuo da função PERMISSIONS pode resultar em desempenho mais lento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
PERMISSIONS ( [ objectid [ , 'column' ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *objectid*  
 É a ID de um protegível. Se *objectid* não for especificada, o valor bitmap conterá permissões de instrução para o usuário atual; caso contrário, o bitmap conterá permissões no protegível para o usuário atual. O protegível especificado deve estar no banco de dados atual. Use a função [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) para determinar o valor de *objectid*.  
  
 **'** *column* **'**  
 É o nome opcional de uma coluna para a qual as informações de permissão são retornadas. A coluna deve ter um nome de coluna válido na tabela especificada por *objectid*.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 PERMISSIONS pode ser usado para determinar se o usuário atual possui as permissões necessárias para executar uma instrução ou para conceder uma permissão com GRANT para outro usuário.  
  
 As informações de permissões retornadas são um bitmap de 32 bits.  
  
 Os 16 bits inferiores refletem permissões concedidas ao usuário e também permissões que são aplicadas aos grupos do Windows ou a funções de servidor fixas das quais o usuário atual é membro. Por exemplo, um valor retornado igual a 66 (valor hexadecimal 0x42), quando nenhuma *objectid* é especificada, indica que o usuário tem permissão para executar as instruções CREATE TABLE (valor decimal 2) e BACKUP DATABASE (valor decimal 64).  
  
 Os 16 bits superiores refletem as permissões que o usuário pode conceder com GRANT a outros usuários. Esses 16 bits superiores são interpretados exatamente como os 16 bits inferiores descritos nas tabelas a seguir, com a exceção de que eles são deslocados para a esquerda em 16 bits (multiplicados por 65536). Por exemplo, 0x8 (valor decimal 8) é o bit que indica a permissão INSERT quando *objectid* é especificada. Enquanto que 0x80000 (valor decimal 524288) indica a capacidade de conceder a permissão GRANT INSERT, porque 524288 = 8 x 65536.  
  
 Por causa das associações em funções, um usuário que não possui a permissão para executar uma instrução pode concedê-la a outro usuário.  
  
 A tabela a seguir mostra os bits que são usados para permissões de instrução (*objectid* não é especificada).  
  
|Bit (decimal)|Bit (hexadecimal)|Permissão de instrução|  
|-----------------|-----------------|--------------------------|  
|1|0x1|CREATE DATABASE (somente no banco de dados mestre)|  
|2|0x2|CREATE TABLE|  
|4|0x4|CREATE PROCEDURE|  
|8|0x8|CREATE VIEW|  
|16|0x10|CREATE RULE|  
|32|0x20|CREATE DEFAULT|  
|64|0x40|BACKUP DATABASE|  
|128|0x80|BACKUP LOG|  
|256|0x100|Reservado|  
  
 A tabela a seguir mostra os bits usados para permissões de objeto que são retornadas somente quando *objectid* é especificada.  
  
|Bit (decimal)|Bit (hexadecimal)|Permissão de instrução|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT ALL|  
|2|0x2|UPDATE ALL|  
|4|0x4|REFERENCES ALL|  
|8|0x8|INSERT|  
|16|0x10|Delete (excluir)|  
|32|0x20|EXECUTE (somente procedimentos)|  
|4096|0x1000|SELECT ANY (pelo menos uma coluna)|  
|8192|0x2000|UPDATE ANY|  
|16384|0x4000|REFERENCES ANY|  
  
 A tabela a seguir mostra os bits usados para permissões de objeto em nível de coluna que são retornadas quando *objectid* e a coluna são especificados.  
  
|Bit (decimal)|Bit (hexadecimal)|Permissão de instrução|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT|  
|2|0x2|UPDATE|  
|4|0x4|REFERENCES|  
  
 NULL é retornado quando um parâmetro especificado é NULL ou não é válido (por exemplo, uma *objectid* ou uma coluna que não existe). Os valores de bit para permissões que não se aplicam (por exemplo, a permissão EXECUTE, bit 0x20, para uma tabela) não são definidos.  
  
 Use o operador bit a bit AND (&) para determinar cada conjunto de bits no bitmap retornado pela função PERMISSIONS.  
  
 O procedimento armazenado de sistema sp_helprotect também pode ser usado para retornar uma lista de permissões para um usuário no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-permissions-function-with-statement-permissions"></a>a. Usando a função PERMISSIONS com permissões de instrução  
 O exemplo a seguir determina se o usuário atual pode executar a instrução `CREATE TABLE`.  
  
```sql  
IF PERMISSIONS()&2=2  
   CREATE TABLE test_table (col1 INT)  
ELSE  
   PRINT 'ERROR: The current user cannot create a table.';  
```  
  
### <a name="b-using-the-permissions-function-with-object-permissions"></a>B. Usando a função PERMISSIONS com permissões de objeto  
 O exemplo a seguir determina se o usuário atual pode inserir uma linha de dados na tabela instrução `Address` do banco de dados `AdventureWorks2012`.  
  
```sql  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&8=8   
   PRINT 'The current user can insert data into Person.Address.'  
ELSE  
   PRINT 'ERROR: The current user cannot insert data into Person.Address.';  
```  
  
### <a name="c-using-the-permissions-function-with-grantable-permissions"></a>C. Usando a função PERMISSIONS com permissões que podem ser concedidas  
 O exemplo a seguir determina se o usuário atual pode conceder a permissão INSERT na tabela `Address` do banco de dados `AdventureWorks2012` para outro usuário.  
  
```sql  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&0x80000=0x80000  
   PRINT 'INSERT on Person.Address is grantable.'  
ELSE  
   PRINT 'You may not GRANT INSERT permissions on Person.Address.';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
