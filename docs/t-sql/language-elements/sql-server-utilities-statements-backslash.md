---
description: Barra invertida (continuação de linha) (Transact-SQL)
title: Barra invertida (continuação de linha) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- escape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3451d6a9346fd1988cdfc509635967017a0b6cb9
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095905"
---
# <a name="backslash-line-continuation-transact-sql"></a>Barra invertida (continuação de linha) (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`\` quebra uma constante de cadeia de caractere, um caractere ou um binário longo, em duas ou mais linhas para facilitar a leitura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
<first section of string> \  
<continued section of string>  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 \<first section of string>  
 É o início de uma cadeia de caracteres.  
  
 \<continued section of string>  
 É a continuação de uma cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
Esse comando retorna a primeira seção e as seções contínuas da cadeia de caracteres como uma cadeia de caracteres, sem a barra invertida. A nova linha após a barra invertida deve ser um caractere de alimentação de linha (U + 000A) ou uma combinação de retorno de carro (U + 000D) e alimentação de linha (U + 000A), nessa ordem. 

## <a name="examples"></a>Exemplos  

### <a name="a-splitting-a-character-string"></a>a. Dividindo uma cadeia de caracteres  

O exemplo a seguir usa uma barra invertida e um retorno de carro para dividir uma cadeia de caracteres em duas linhas.  
  
```sql  
SELECT 'abc\  
def' AS [ColumnResult];  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    

### <a name="b-splitting-a-binary-string"></a>B. Dividindo uma cadeia de caracteres binária  

O exemplo a seguir usa uma barra invertida e um retorno de carro para dividir uma cadeia de caracteres binária em duas linhas.  

```sql  
SELECT 0xabc\
def AS [ColumnResult];  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 0xABCDEF
 ```    

## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40;Division&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40;Division Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  
