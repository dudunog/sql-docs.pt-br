---
title: Expressões aritméticas (XQuery) | Microsoft Docs
description: Saiba mais sobre expressões aritméticas em XQuery e quais operadores aritméticos têm suporte.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 548fde62cf6f07d2e31a68b7f702baa4bd9f916a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643661"
---
# <a name="arithmetic-expressions-xquery"></a>Expressões aritméticas (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Todos os operadores aritméticos têm suporte, exceto para **IDIV**. Os exemplos a seguir ilustram o uso básico dos operadores aritméticos:  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 Como não há suporte para **IDIV** , uma solução é usar o construtor **xs: Integer ()** :  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 O tipo resultante de um operador aritmético é baseado nos tipos dos valores de entrada. Se os operandos forem de tipos diferentes, qualquer um dos dois, ou ambos, quando necessário serão convertidos em um tipo de base primitivo comum, de acordo com a hierarquia do tipo. Para obter informações sobre a hierarquia de tipos, consulte [regras de conversão de tipo em XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 Promoção de tipo numérico ocorre se as duas operações forem de tipos de base numéricos diferentes. Por exemplo, adicionar um **xs: decimal** a um **xs: Double** primeiro alteraria o valor decimal para Double. Em seguida, a adição seria executada de forma a resultar em um valor duplo.  
  
 Os valores atômicos não tipados são convertidos no tipo de base numérico do outro operando ou em **xs: Double** se o outro operando também não for digitado.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Os argumentos para os operadores aritméticos devem ser do tipo numeric ou **untypedAtomic**.  
  
-   Operações em **xs: valores inteiros** resultam em um valor do tipo **xs: decimal** em vez de **xs: integer**.  
  
  
