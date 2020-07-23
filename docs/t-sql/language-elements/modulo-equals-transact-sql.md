---
title: '%= (Atribuição de módulo) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%=_TSQL'
- '%='
dev_langs:
- TSQL
helpviewer_keywords:
- '%= (modulo equals)'
- '%= (modulus assignment)'
- compound operators, %=
- assignment operators, %=
- augmented operators, %=
ms.assetid: 45e35516-1f4c-406b-a580-70a14b087847
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c24c56506cbb2ecd85a7d112ee82edb3c7fa70c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922894"
---
# <a name="-modulus-assignment-transact-sql"></a>%= (Atribuição de módulo) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Divide um número por outro e define um valor como o resultado da operação. Por exemplo, se uma variável @x for igual a 38, @x %= 5 usará o valor original de @x, dividirá esse valor por 5 e definirá @x com o resto dessa divisão (3).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression %= expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de qualquer um dos tipos de dados na categoria numérica, com exceção do tipo de dados **bit**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações, consulte [% &#40;Módulo&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
