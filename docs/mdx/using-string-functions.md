---
title: Usando funções de cadeia de caracteres | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74eec478baad335cb5be6a78ec1faea2d15030ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037989"
---
# <a name="using-string-functions"></a>Usando as funções de cadeia de caracteres


  Você pode usar as funções de cadeia de caracteres em praticamente todos os objetos em Multidimensional Expressions (MDX). Em procedimentos armazenados, use as funções de cadeia de caracteres principalmente para converter o objeto em uma representação de cadeia de caracteres. Também é possível usar as funções de cadeia de caracteres para avaliar uma expressão de cadeia de caracteres sobre um objeto para retornar um valor.  
  
 As funções de cadeia de caracteres usadas mais amplamente são **Name** e **UniqueName**. Respectivamente, estas funções retornam o nome e o nome exclusivo de um objeto. Elas são usadas principalmente ao depurar cálculos para identificar qual membro está sendo retornando por uma função.  
  
## <a name="examples"></a>Exemplos  
 As consultas de exemplo a seguir mostram como usar estas funções:  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 A função **Generate** pode ser usada para executar uma função de cadeia de caracteres em cada membro de um conjunto e concatenar os resultados. Isto também pode ser útil ao depurar cálculos, pois permite visualizar o conteúdo de um conjunto. O exemplo a seguir mostra como usá-la desse modo:  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Outro grupo de funções de cadeia de caracteres usadas com frequência são as que permitem converter uma cadeia de caracteres que contém o nome exclusivo de um objeto ou uma expressão que resolve o objeto no próprio objeto. A consulta de exemplo a seguir demonstra como as funções **StrToMember** e **StrToSet** fazem isso:  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  As funções **StrToMember** e **StrToSet** devem ser usadas com cautela. Elas podem gerar um desempenho de consulta insatisfatório se forem usadas em definições de cálculo.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerar &#40;MDX&#41;](../mdx/generate-mdx.md)   
 [Nome &#40;&#41;MDX](../mdx/name-mdx.md)   
 [UniqueName&#41;MDX &#40;](../mdx/uniquename-mdx.md)   
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usando procedimentos armazenados &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember&#41;MDX &#40;](../mdx/strtomember-mdx.md)   
 [StrToSet&#41;MDX &#40;](../mdx/strtoset-mdx.md)  
  
  
