---
title: FILE_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_NAME_TSQL
- FILE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file names
- file names [SQL Server], FILE_NAME
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- displaying file names
- identification numbers [SQL Server], files
- FILE_NAME function
- logical file names [SQL Server]
ms.assetid: 68b298aa-ce47-4af5-b59f-9a1b46d48326
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f47e9c58921cbbf473295e62cc78f9bbd99f714
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112457"
---
# <a name="file_name-transact-sql"></a>FILE_NAME (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Essa função retorna o nome de arquivo lógico para o número de identificação (ID) de arquivo fornecido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FILE_NAME ( file_id )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*file_id*  
Número de identificação de arquivos cujo nome de arquivo será retornado por `FILE_NAME`. *file_id* tem um tipo de dados **int**.  
  
## <a name="return-types"></a>Tipos de retorno  
**nvarchar(128)**  
  
## <a name="remarks"></a>Comentários  
*file_ID* corresponde à coluna file_id na exibição do catálogo sys. master_files ou a exibição do catálogo sys. database_files.  
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna os nomes de arquivo para `file_ID 1` e `file_ID` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT FILE_NAME(1) AS 'File Name 1', FILE_NAME(2) AS 'File Name 2';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
File Name 1                File Name 2  
-------------------------  ------------------------  
AdventureWorks2012_Data    AdventureWorks2012_Log  

(1 row(s) affected)
``` 
  
## <a name="see-also"></a>Consulte Também  
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
