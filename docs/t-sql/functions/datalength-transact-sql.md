---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac8f7372833d70a46e5ea3cb343641b02aa05120
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113086"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna o número de bytes usado para representar qualquer expressão.

> [!NOTE]
> Para retornar o número de caracteres em uma expressão de cadeia de caracteres, use a função [LEN](../../t-sql/functions/len-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
DATALENGTH ( expression )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*expressão*  
É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de dados.
  
## <a name="return-types"></a>Tipos de retorno
**bigint** se *expression* tiver um tipo de dados **nvarchar(max)** , **varbinary(max)** ou **varchar(max)** ; caso contrário, **int**.
  
## <a name="remarks"></a>Comentários  
`DATALENGTH` torna-se muito útil quando usada com tipos de dados que podem armazenar dados de comprimento variável, como:
- **imagem**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**
- **varchar**
  
Para um valor NULL, `DATALENGTH` retorna NULL.
  
> [!NOTE]  
> Os níveis de compatibilidade podem afetar os valores de retorno. Veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) para obter mais informações sobre níveis de compatibilidade.  

> [!NOTE]
> Use [LEN](../../t-sql/functions/len-transact-sql.md) para retornar o número de caracteres codificados em determinada expressão de cadeia de caracteres e [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) para retornar o tamanho em bytes de determinada expressão de cadeia de caracteres. Essas saídas podem ser diferentes dependendo do tipo de dados e do tipo de codificação usado na coluna. Para obter mais informações sobre as diferenças de armazenamento entre diferentes tipos de codificação, confira [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

## <a name="examples"></a>Exemplos  
Este exemplo localiza o comprimento da coluna `Name` na tabela `Product`:
  
```sql
USE AdventureWorks2016  
GO
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Confira também
[LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
