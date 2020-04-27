---
title: Contexto de cálculo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aec8aa98-b77d-4f8f-9684-2618b1d8e970
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 847e9da07f8c255af8041071c63254b241490761
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074684"
---
# <a name="calculation-context"></a>Contexto de cálculo
  O contexto de cálculo é o subespaço conhecido do cubo onde uma expressão é avaliada e todas as coordenadas são explicitamente conhecidas ou podem ser derivadas da expressão.  
  
## <a name="determining-the-calculation-context"></a>Determinando o contexto de cálculo  
 Cada conjunto, membro, tupla, ou função numérica é executado no contexto de toda a expressão ou instrução MDX. Quando um argumento, como uma tupla, é transmitido para uma função, somente algumas das coordenadas no espaço do cubo são explicitamente fornecidas. As outras coordenadas são obtidas com base no contexto de cálculo atual.  
  
 O contexto de cálculo para coordenadas de célula não especificada e membros de atributo é determinado na seguinte ordem:  
  
1.  A cláusula FROM (se aplicável) – essa cláusula pode especificar um cubo inteiro ou pode especificar um subcubo na forma de uma instrução SELECT.  
  
2.  A cláusula WHERE (se aplicável) – essa cláusula, também conhecida como *eixo de segmentação*, em que você especifica um conjunto, tupla ou membro que restringe os membros retornados no eixo da coluna e eixo de linhas em uma consulta. Conceitualmente, o membro padrão de cada hierarquia de atributo que não é especificado explicitamente no eixo da coluna ou no eixo de linhas faz parte do eixo do slicer.  
  
    > [!NOTE]  
    >  Quando as coordenadas da célula de um atributo específico são especificadas no eixo do slicer e em outro eixo, as coordenadas especificadas na função podem ter prioridade ao determinar os membros do conjunto no eixo. As funções [Filter (MDX)](/sql/mdx/filter-mdx) e [Order (MDX)](/sql/mdx/order-mdx) são exemplos dessas funções – você pode filtrar ou pode ordenar um resultado por membros de atributo que são excluídos do contexto de cálculo pela cláusula WHERE, ou por uma instrução SELECT na cláusula FROM.  
  
3.  Os conjuntos nomeados e membros calculados definidos na consulta ou na expressão.  
  
4.  As tuplas e conjuntos especificados nos eixos de linhas e da coluna, utilizando o membro padrão para atributos que não aparecem no eixo de linha, coluna ou do slicer.  
  
5.  As células de cubo ou subcubo em cada eixo, eliminando tuplas vazias no eixo e aplicando a cláusula HAVING.  
  
6.  Para obter mais informações, consulte [Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md).  
  
 Na consulta a seguir, o contexto de cálculo para o eixo de linha é restrito pelo membro de atributo País e pelo membro de atributo Ano Civil que são especificados na cláusula WHERE.  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 Porém, se você modificar essa consulta especificando a função `FILTER` no eixo de linhas, e utilizar um membro de hierarquia de atributo Ano Civil na função `FILTER`, o membro de atributo da hierarquia de atributo Ano Civil que é usada para fornecer o contexto de cálculo aos membros do conjunto no eixo da coluna poderá ser modificado.  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 Na consulta anterior, o contexto de cálculo para as células nas tuplas que aparecem no eixo da coluna é filtrado pelo membro CY 2003 da hierarquia de atributo Ano Civil, mesmo se o contexto de cálculo nominal da hierarquia de atributo Ano Civil for CY 2004. Além disso, o contexto é filtrado pela medida Quantidade de Pedidos pela Internet. No entanto, assim que os membros do conjunto no eixo da coluna são definidos, o contexto de cálculo dos valores dos membros que aparecem no eixo é novamente determinado pela cláusula WHERE.  
  
> [!IMPORTANT]  
>  Para aprimorar o desempenho da consulta, você deve eliminar membros e tuplas no processo de resolução o quanto antes. Dessa forma, cálculos complexos de tempo de consulta no conjunto final de membros operam com o menor número possível de células.  
  
## <a name="see-also"></a>Consulte Também  
 [Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
  
