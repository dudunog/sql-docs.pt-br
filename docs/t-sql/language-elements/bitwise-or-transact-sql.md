---
description: '| (OR bit a bit) (Transact-SQL)'
title: '| (OR bit a bit) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dce8843b20df446172db47a8d07fdb0ecf4b296
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459430"
---
# <a name="-bitwise-or-transact-sql"></a>| (OR bit a bit) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Executa uma operação OR lógica bit a bit entre dois valores inteiros especificados, conforme convertidos em expressões binárias dentro de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```   
expression | expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida da categoria de tipo de dados inteiro ou dos tipos de dados **bit**, **binary** ou **varbinary**. *expression* é tratada como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Apenas uma *expression* pode ser do tipo de dados **binary** ou **varbinary** em uma operação bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna um **int** se os valores de entrada são **int**, um **smallint** se os valores de entrada são **smallint** ou um **tinyint** se os valores de entrada são **tinyint**.  
  
## <a name="remarks"></a>Comentários  
 O operador bit a bit | executa um OR lógico bit a bit entre as duas expressões, usando cada bit correspondente para as duas expressões. Os bits no resultado serão definidos como 1 se um ou os dois bits (para o bit atual a ser resolvido) nas expressões de entrada tiverem o valor 1; se nenhum bit nas expressões de entrada for 1, o bit no resultado será definido como 0.  
  
 Se as expressões à esquerda e à direita tiverem tipos de dados inteiros diferentes (por exemplo, a *expression* à esquerda é **smallint** e a *expression* à direita é **int**), o argumento do tipo de dados menor será convertido no tipo de dados maior. Neste exemplo, a **smallint**_expression_ é convertida em um **int**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela com tipos de dados **int** para mostrar os valores originais e coloca a tabela em uma linha.  
  
```sql  
CREATE TABLE bitwise (  
  a_int_value INT NOT NULL,  
  b_int_value INT NOT NULL);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 A consulta a seguir executa o OR bit a bit nas colunas **a_int_value** e **b_int_value**.  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 A representação binária de 170 (**a_int_value** ou `A`, abaixo) é `0000 0000 1010 1010`. A representação binária de 75 (**b_int_value** ou `B`, abaixo) é `0000 0000 0100 1011`. A execução da operação OR bit a bit nesses dois valores produz o resultado binário `0000 0000 1110 1011`, que é o decimal 235.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124;= &#40;Atribuição de OR bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


