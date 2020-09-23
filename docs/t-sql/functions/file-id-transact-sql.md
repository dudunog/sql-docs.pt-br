---
description: FILE_ID (Transact-SQL)
title: FILE_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_ID
- FILE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], files
- file IDs [SQL Server]
- FILE_ID function
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_ID
ms.assetid: 6a7382cf-a360-4d62-b9d2-5d747f56f076
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9cdd99caf69ce254e1a42d345526515d2fb0472f
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115493"
---
# <a name="file_id-transact-sql"></a>FILE_ID (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Para o nome lógico específico para um arquivo de componente do banco de dados atual, essa função retorna o número de identificação (ID) do arquivo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
FILE_ID ( file_name )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*file_name*  
Uma expressão do tipo **sysname**, que representa o nome lógico do arquivo cujo valor de ID de arquivo será retornado por `FILE_ID`.  
  
## <a name="return-types"></a>Tipos de retorno  
**smallint**  
  
## <a name="remarks"></a>Comentários  
*file_name* corresponde ao nome de arquivo lógico exibido na coluna name nas exibições do catálogo sys.master_files ou sys.database_files.  

O `FILE_ID` retorna `NULL` se *file_name* não corresponde ao nome lógico de um arquivo de componente do banco de dados atual.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número de identificação de arquivo atribuído a catálogos de texto completo excede 32767. Como a função `FILE_ID` tem um tipo de retorno **smallint**, `FILE_ID` não dará suporte a arquivos de texto completo. Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o valor de ID de arquivo para o arquivo `AdventureWorks_Data`, um arquivo de componente do banco de dados `ADVENTUREWORKS2012`.  

```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_ID('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [FILE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
