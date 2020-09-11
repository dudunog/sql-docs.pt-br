---
description: CHECKSUM (Transact-SQL)
title: CHECKSUM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d9d8db55081e82657966e98a22345076bdd83108
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459855"
---
# <a name="checksum-transact-sql"></a>CHECKSUM (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

A função `CHECKSUM` retorna o valor de soma de verificação computado em uma linha da tabela, ou em uma lista de expressões. Use `CHECKSUM` para criar índices de hash.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
\*  
Esse argumento especifica que o cálculo da soma de verificação abrange todas as colunas de tabela. `CHECKSUM` retorna um erro se uma coluna tem um tipo de dados não comparável. Os tipos de dados não comparáveis incluem:

- **cursor**
- **imagem**
- **ntext**
- **text**
- **XML**

Outro tipo de dados não comparável é **sql_variant** com qualquer um dos tipos de dados anteriores como seu tipo base.
  
*expressão*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo, com exceção de um tipo de dados não comparável.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários  
`CHECKSUM` calcula um valor de hash, chamado de soma de verificação, em sua lista de argumentos. Use esse valor de hash para criar índices de hash. Um índice de hash ocorrerá se a função `CHECKSUM` tiver argumentos de coluna e um índice for criado com base no valor de `CHECKSUM` calculado. Isso pode ser usado para pesquisas de igualdade em colunas.
  
A função `CHECKSUM` atende às propriedades da função de hash: `CHECKSUM` aplicado a duas listas de expressões retornarão o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo de dados e se esses elementos correspondentes tiverem igualdade quando comparados com o operador de igualdade (=). Valores nulos de um tipo especificado são definidos para serem comparados como iguais para fins da função `CHECKSUM`. Se pelo menos um dos valores na lista de expressões for alterado, a soma de verificação de lista provavelmente será alterada. No entanto, isso não é garantido. Portanto, para detectar se os valores foram alterados, recomendamos o uso de `CHECKSUM` somente se o aplicativo puder tolerar uma alteração ausente ocasional. Caso contrário, considere a possibilidade de usar o `HASHBYTES`. Com um algoritmo de hash MD5 especificado, a probabilidade de que `HASHBYTES` retornará o mesmo resultado para duas entradas diferentes é muito menor em comparação com `CHECKSUM`.
  
A ordem de expressão afeta o valor `CHECKSUM` computado. A ordem das colunas usada para `CHECKSUM(*)` é a mesma especificada na definição de tabela ou exibição. Isso inclui as colunas computadas.
  
O valor de `CHECKSUM` depende da ordenação. O mesmo valor armazenado com uma ordenação diferente retornará um valor de `CHECKSUM` diferente.
  
`CHECKSUM ()` não garante resultados exclusivos.

## <a name="examples"></a>Exemplos  
Estes exemplos mostram o uso de `CHECKSUM` para criar índices de hash.
  
Para criar o índice de hash, o primeiro exemplo adiciona uma coluna de soma de verificação computada à tabela que você deseja indexar. Em seguida, ele cria um índice na coluna de soma de verificação. 
  
```sql
-- Create a checksum index.  

SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
Este exemplo mostra o uso de um índice de soma de verificação como um índice de hash. Isso pode ajudar a melhorar a velocidade de indexação quando a coluna a ser indexada é uma coluna de caracteres longa. O índice de soma de verificação pode ser usado para pesquisas de igualdade.
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  

SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
A criação do índice na coluna computada materializa a coluna de soma de verificação e todas as alterações no valor de `ProductName` serão propagadas para a coluna de soma de verificação. Como alternativa, podemos criar um índice diretamente na coluna que desejamos indexar. No entanto, para valores de chave longos, um índice normal provavelmente não terá o mesmo desempenho que um índice de soma de verificação.
  
## <a name="see-also"></a>Veja também
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  
