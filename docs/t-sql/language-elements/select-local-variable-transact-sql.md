---
title: SELECT @local_variable (Transact-SQL)
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
author: rothja
ms.author: jroth
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||= azure-sqldw-latest||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: dac349e757e563068a69f938c5343df8998a9b1f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395775"
---
# <a name="select-local_variable-transact-sql"></a>SELECT @local_variable (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Define uma variável local com o valor de uma expressão.  
  
 Para atribuir variáveis, recomendamos o uso de [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md), em vez de SELECT @*local_variable*.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

@*local_variable*  
 É uma variável declarada para a qual um valor será atribuído.  
  
{= \| += \| -= \| \*= \| /= \| %= \| &= \| ^= \| \|= }  
Atribui o valor à direita à variável da esquerda.  
  
Operador de atribuição composto:  

| operador | ação |  
| -------- | ------ |  
| = | Atribui a expressão a seguir à variável. |  
| += | Adicionar e atribuir |  
| -= | Subtrair e atribuir |  
| \*= | Multiplicar e atribuir |  
| /= | Dividir e atribuir |  
| %= | Módulo e atribuir |  
| &= | AND bit a bit e atribuir |  
| ^= | XOR bit a bit e atribuir |  
| \|= | OR bit a bit e atribuir |  

*expressão*  
É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida. Isso inclui uma subconsulta escalar.  

## <a name="remarks"></a>Comentários

SELECT @*local_variable* normalmente é usado para retornar um único valor na variável. No entanto, quando *expression* é o nome de uma coluna, ela pode retornar vários valores. Se a instrução SELECT retornar mais de um valor, à variável será atribuído o último valor retornado.  

Se a instrução SELECT não retornar nenhuma linha, a variável reterá seu valor atual. Se *expression* for uma subconsulta escalar que não retorna nenhum valor, a variável será definida como NULL.  

Uma instrução SELECT pode inicializar várias variáveis locais.  

> [!NOTE]
> Uma instrução SELECT que contém uma atribuição de variável não pode ser usada também para executar operações típicas de recuperação de conjunto de resultados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-use-select-local_variable-to-return-a-single-value"></a>a. Usar SELECT @local_variable para retornar um único valor  
 No exemplo a seguir, a variável `@var1` recebe `Generic Name` com seu valor. A consulta na tabela `Store` não retorna linhas porque o valor especificado para `CustomerID` não existe na tabela. A variável retém o valor `Generic Name`.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-local_variable-to-return-null"></a>B. Usar SELECT @local_variable para retornar nulo  
 No exemplo a seguir, uma subconsulta é usada para atribuir um valor a `@var1`. Como o valor solicitado para `CustomerID` não existe, a subconsulta não retorna valores e a variável é definida como `NULL`.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
