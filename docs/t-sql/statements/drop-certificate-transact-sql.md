---
description: DROP CERTIFICATE (Transact-SQL)
title: DROP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP CERTIFICATE
- DROP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], removing
- removing certificates
- dropping certificates
- DROP CERTIFICATE statement
- deleting certificates
ms.assetid: 5704aa04-68a3-4b29-b62b-8868af487817
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b752d29f38bd6a4301ea4f5da2a3560c02608bb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483898"
---
# <a name="drop-certificate-transact-sql"></a>DROP CERTIFICATE (Transact-SQL)
[!INCLUDE [sql-asdb-pdw](../../includes/applies-to-version/sql-asdb-pdw.md)]

  Remove um certificado do banco de dados.  
  
> [!IMPORTANT]  
>  Um backup do certificado usado para criptografia de banco de dados deverá ser mantido até mesmo se a criptografia não estiver mais habilitada em um banco de dados. Mesmo que o banco de dados não esteja mais criptografado, partes do log de transações ainda poderão permanecer protegidas e talvez o certificado seja necessário para algumas operações até a realização do backup completo do banco de dados. O certificado também é necessária para que seja possível restaurar os backups criados no momento em que o banco de dados estava criptografado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md) 

  
 
## <a name="syntax"></a>Sintaxe  
  
```synaxsql  
DROP CERTIFICATE certificate_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *certificate_name*  
 É o nome exclusivo pelo qual o certificado é conhecido no banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Certificados só poderão ser descartados se nenhuma entidade estiver associada a eles.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no certificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o certificado `Shipping04` do banco de dados `AdventureWorks`.  
  
```sql  
USE AdventureWorks2012;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir descarta o certificado `Shipping04`.  
  
```sql
USE master;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
