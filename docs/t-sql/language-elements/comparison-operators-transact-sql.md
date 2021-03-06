---
description: Operadores de comparação (Transact-SQL)
title: Operadores de comparação (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
author: cawrites
ms.author: chadam
ms.openlocfilehash: 51d1afb08dc3ea9bd40a968aa76c2b64e06989f1
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092168"
---
# <a name="comparison-operators-transact-sql"></a>Operadores de comparação (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Os operadores de comparação testam se duas expressões são iguais. Os operadores de comparação podem ser usados em todas as expressões, exceto em expressões dos tipos de dados **text**, **ntext** ou **image**. A tabela a seguir lista os operadores de comparação [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Operador|Significado|  
|--------------|-------------|  
|[= (Igual a)](../../t-sql/language-elements/equals-transact-sql.md)|Igual a|  
|[> (Maior que)](../../t-sql/language-elements/greater-than-transact-sql.md)|Maior que|  
|[< (Menor que)](../../t-sql/language-elements/less-than-transact-sql.md)|Menor que|  
|[>= (Maior ou igual a)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|Maior ou igual a|  
|[<= (Menor ou igual a)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|Menor que ou igual a|  
|[<> (Diferente de)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|É diferente de|  
|[!= (Diferente de)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|Diferente de (não é padrão ISO)|  
|[\!< (Não é menor que)](../../t-sql/language-elements/not-less-than-transact-sql.md)|Não é menor que (não é padrão ISO)|  
|[\!> (Não é maior que)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|Não é maior que (não é padrão ISO)|  
  
## <a name="boolean-data-type"></a>Tipo de dados booliano  
 O resultado de um operador de comparação tem o tipo de dados **Boolean**. Ele tem três valores: TRUE, FALSE e UNKNOWN. Expressões que retornam um tipo de dados **Boolean** são conhecidas como expressões boolianas.  
  
 Ao contrário de outros tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um tipo de dados **Boolean** não pode ser especificado como o tipo de dados de uma variável ou coluna de tabela e não pode ser retornado em um conjunto de resultados.  
  
 Quando SET ANSI_NULLS é ON, um operador com uma ou duas expressões NULL retorna UNKNOWN. Quando SET ANSI_NULLS estiver desativado, as mesmas regras serão aplicáveis, exceto para os operadores igual a (=) e não igual a (<>). Quando SET ANSI_NULLS estiver desativado, esses operadores tratarão NULL como um valor conhecido, equivalente a qualquer outro NULL, e retornarão apenas TRUE ou FALSE (nunca UNKNOWN).  
  
 Expressões com tipos de dados **Boolean** são usadas na cláusula WHERE para filtrar as linhas que se qualificam para os critérios de pesquisa e nas instruções de linguagem de controle de fluxo, como IF e WHILE, por exemplo:  
  
```syntaxsql  
-- Uses AdventureWorks  
  
DECLARE @MyProduct INT;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
