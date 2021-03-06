---
description: COL_NAME (Transact-SQL)
title: COL_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
author: cawrites
ms.author: chadam
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 003629030dfd9fdaeab4f98ced539609c5a4cabc
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101340"
---
# <a name="col_name-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna o nome de uma coluna de tabela com base nos valores de número de identificação de tabela e número de identificação de coluna daquela coluna da tabela.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
COL_NAME ( table_id , column_id )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*table_id*  
O número de identificação da tabela que contém aquela coluna. O argumento *table_id* tem um tipo de dados **int**.
  
*column_id*  
O número de identificação da coluna. O argumento *column_id* tem um tipo de dados **int**.
  
## <a name="return-types"></a>Tipos de retorno
**sysname**
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver a permissão correta para exibir o objeto.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário pode exibir apenas os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha recebido permissão. Isso significa que as funções internas que emitem metadados, como `COL_NAME`, poderão retornar NULL se o usuário não tiver as permissões corretas para o objeto. Veja [Configuração de Visibilidade de Metadados](../../relational-databases/security/metadata-visibility-configuration.md) para obter mais informações.
  
## <a name="remarks"></a>Comentários  
Os parâmetros de *table_id* e *column_id* juntos produzem uma cadeia de caracteres de nome de coluna.
  
Veja [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md) para obter mais informações sobre como obter números de identificação de tabela e de coluna.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o nome da primeira coluna em uma tabela `Employee` de amostra.
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>Confira também
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  

