---
title: Criando conjuntos nomeados no escopo da consulta (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- query-scoped named sets [MDX]
- WITH keyword
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a611d3d20d269bb9c3fa3a1f764181b1660713b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074066"
---
# <a name="creating-query-scoped-named-sets-mdx"></a>Criando conjuntos nomeados no escopo da consulta (MDX)
  Se um conjunto nomeado for necessário para uma única consulta MDX, é possível defini-lo usando a palavra-chave WITH. O conjunto nomeado criado com a palavra-chave WITH deixará de existir ao fim da execução da consulta.  
  
 Como discutido neste tópico, a sintaxe da palavra-chave WITH é bem flexível, comportando até o uso de funções para definir o conjunto nomeado.  
  
> [!NOTE]  
>  Para obter mais informações sobre conjuntos nomeados, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](mdx-named-sets-building-named-sets.md).  
  
## <a name="with-keyword-syntax"></a>Sintaxe da palavra-chave WITH  
 Use a sintaxe a seguir para adicionar a palavra-chave WITH a uma instrução MDX SELECT:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 Na sintaxe para a palavra-chave WITH, o parâmetro `Set_Identifier` contém o alias do conjunto nomeado. O parâmetro `Set_Expression` contém a expressão de conjunto à qual se refere o alias do conjunto nomeado.  
  
## <a name="with-keyword-example"></a>Exemplo da palavra-chave WITH  
 A consulta MDX a seguir examina a venda unitária dos diversos vinhos Chardonnay e Chablis em `FoodMart 2000`, o banco de dados de exemplo do Microsoft SQL Server 2000 Analysis Services. Essa consulta, embora bem simples em termos de conjunto de resultados, é longa e complicada quando requer manutenção.  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 Para facilitar a manutenção da consulta MDX anterior, você pode criar um conjunto nomeado para ela usando a palavra-chave WITH. O código a seguir mostra como usar a palavra-chave WITH para criar um conjunto nomeado, `[ChardonnayChablis]`, e como o conjunto nomeado torna a manutenção da instrução SELECT mais rápida e fácil.  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### <a name="using-functions-together-with-the-with-keyword"></a>Usando funções com a palavra-chave WITH  
 Embora seja possível definir explicitamente cada membro de um conjunto nomeado, essa abordagem pode produzir uma instrução extensa. Para facilitar a criação e a manutenção de um conjunto nomeado, use as funções MDX para definir os membros.  
  
 Por exemplo, o exemplo de consulta MDX a seguir usa as funções MDX [Filter](/sql/mdx/filter-mdx), [CurrentMember](/sql/mdx/current-mdx)e [Name](/sql/mdx/members-string-mdx) e a função VBA InStr para criar o conjunto nomeado `[ChardonnayChablis]` . Essa versão do conjunto nomeado `[ChardonnayChablis]` é igual àquela definida explicitamente e mostrada anteriormente neste tópico.  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Criando conjuntos nomeados no escopo da sessão &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  
