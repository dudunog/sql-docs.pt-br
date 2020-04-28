---
title: Expressões (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a1dfcdc52bb52652c204e31c28ccf5ec48ca7a00
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893594"
---
# <a name="expressions-mdx"></a>Expressões (MDX)


  Uma expressão é uma combinação de identificadores, valores e operadores que podem ser avaliados para obter um resultado. Os dados podem ser usados em diversos locais diferentes ao acessar ou alterar dados. Por exemplo, você pode usar uma expressão como parte dos dados a serem recuperados em uma consulta ou como um critério de pesquisa ao procurar dados que atendam a um conjunto de critérios.  
  
## <a name="simple-and-complex-expressions"></a>Expressões Simples e Complexas  
 Uma expressão pode ser simples ou complexa no MDX:  
  
 A expressão simples pode ser uma das seguintes expressões:  
  
 Constante  
 Uma constante é um símbolo que representa um valor simples e específico em MDX. Valores de cadeia de caracteres, numéricos e de data podem ser processados como constantes. Ao contrário das constantes numéricas, as constantes de cadeia de caracteres e data devem ser delimitadas com aspas simples (').  
  
 Função de valor escalar  
 Uma função de valor escalar retorna um valor simples dentro do contexto de avaliação em MDX. Essa distinção é importante para compreender como o MDX resolve as funções de valores escalares, pois a maioria das expressões, instruções e scripts do MDX é avaliada não sobre o elemento de dados simples, mas de forma iterativa sobre um grupo de elementos de dados, como células ou membros. Entretanto, na ocasião em que a função de valor escalar é avaliada, a função normalmente está revisando um elemento de dados simples.  
  
 Identificador de objeto  
 O MDX é orientado por objeto devido à sua natureza de dados multidimensionais. Os identificadores de objeto são considerados expressões simples em DMX. Para obter mais informações sobre identificadores, consulte [identificadores &#40;MDX&#41;](../mdx/identifiers-mdx.md).  
  
 Uma expressão complexa também pode ser criada a partir das combinações dessas entidades unidas por operadores.  
  
## <a name="expression-results"></a>Resultados da expressão  
 Em uma expressão simples criada de uma simples constante, variável, função de valor escalar ou nome de coluna simples, o tipo de dados, a ordenação, a precisão, a escala e o valor da expressão é o tipo de dados, ordenação, precisão, escala e valor do elemento consultado. Como o MDX oferece suporte direto apenas ao tipo de dados OLE VARIANT, a coerção não deveria ocorrer ao trabalhar com expressões simples.  
  
 Em uma expressão complexa, a coerção pode ocorrer ao usar duas ou mais expressões simples com tipos de dados diferentes.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 A consulta a seguir mostra exemplos de medidas calculadas cujas definições são expressões simples:  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Uma expressão também pode ser um cálculo, como `[Measures].[Discount Amount] * 1.5`. O exemplo a seguir demonstra o uso de um cálculo para definir um membro em uma instrução SELECT do MDX:  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Usando expressões de cubo e subcubo](../mdx/using-cube-and-subcube-expressions.md)|Define as expressões de cubo e subcubo.|  
|[Usando expressões de dimensão](../mdx/using-dimension-expressions.md)|Define as expressões de dimensão.|  
|[Usando expressões de membros](../mdx/using-member-expressions.md)|Define as expressões de membro.|  
|[Usando expressões de tupla](../mdx/using-tuple-expressions.md)|Define as expressões de tupla.|  
|[Usando expressões de conjunto](../mdx/using-set-expressions.md)|Define as expressões fixas.|  
|[Usando expressões escalares](../mdx/using-scalar-expressions.md)|Define as expressões de valor escalar.|  
|[Trabalhando com valores vazios](../mdx/working-with-empty-values.md)|Descreve o que é um valor vazio e como tais valores são controlados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de linguagem MDX &#40;&#41;MDX](../mdx/mdx-language-reference-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)  
  
  
