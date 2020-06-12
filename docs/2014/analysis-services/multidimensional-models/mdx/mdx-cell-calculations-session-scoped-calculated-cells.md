---
title: Criando células calculadas no escopo da sessão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
author: minewiskan
ms.author: owend
ms.openlocfilehash: 199de07778a153cd1bc40b5033d364e5e0055bd3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546428"
---
# <a name="creating-session-scoped-calculated-cells"></a>Criando células calculadas no escopo da sessão
    
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Para criar células calculadas disponíveis para todas as consultas da mesma sessão, você pode usar a instrução [CREATE CELL CALCULATION](/sql/mdx/mdx-data-definition-create-cell-calculation) ou a instrução [ALTER CUBE](/sql/mdx/mdx-data-definition-alter-cube) . Ambas produzem o mesmo resultado.  
  
## <a name="create-cell-calculation-syntax"></a>Sintaxe de CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Use a sintaxe a seguir para usar a instrução CREATE CELL CALCULATION para definir uma célula calculada no escopo da sessão:  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>Sintaxe de ALTER CUBE  
  
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Use a sintaxe a seguir para usar a instrução ALTER CUBE para definir uma célula calculada no escopo da sessão:  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 O valor `String_Expression` contém uma lista de expressões de conjunto MDX ortogonais e unidimensionais, sendo que cada uma deve resolver uma das categorias de conjuntos listadas na tabela a seguir.  
  
|Categoria|Descrição|  
|--------------|-----------------|  
|Conjunto vazio|Uma expressão de conjunto MDX resolvida em um conjunto vazio. Nesse caso, o escopo da célula calculada é o cubo inteiro.|  
|Conjunto de membro único|Uma expressão de conjunto MDX resolvida em um único membro.|  
|Conjunto de membros do nível|Uma expressão de conjunto MDX resolvida nos membros de um mesmo nível. Um exemplo disso é a *Level_Expression*.`Members` Função MDX. Para incluir membros calculados, use o *Level_Expression*.`AllMembers` Função MDX.<br /><br /> Para obter mais informações, consulte [AllMembers &#40;MDX&#41;](/sql/mdx/allmembers-mdx).|  
|Conjunto de descendentes|Uma expressão de conjunto MDX resolvida nos descendentes de um membro especificado. Um exemplo disso é a `Descendants` função MDX (*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Para obter mais informações, consulte [Descendants &#40;MDX&#41;](/sql/mdx/descendants-mdx).|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando cálculos de célula em MDX &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
