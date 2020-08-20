---
description: ValidMeasure (MDX)
title: ValidMeasure (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd2bc2385a3445076636fb1b4001120463d1cd89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494820"
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)


  Retorna o valor de uma medida em um cubo, forçando dimensões inaplicáveis para o nível Todos (ou o membro padrão, se não agregável) durante o retorno de resultados para uma tupla especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Comentários  
 A função **ValidMeasure** retorna o valor de uma tupla, ignorando atributos que não têm nenhuma relação com o grupo de medidas da medida cujo valor a tupla retorna. Um atributo pode não estar relacionado a uma medida por dois motivos:  
  
-   A dimensão do atributo não tem relação com o grupo de medidas da medida na tupla.  
  
-   A dimensão do atributo não tem uma relação com o grupo de medidas da medida, mas o atributo de granularidade não é o atributo de chave, e o atributo de granularidade não tem uma relação direta com o atributo na tupla.  
  
 O comportamento especificado por essa função é o comportamento padrão do lado do servidor e é controlado pela propriedade **IgnoreUnrelatedDimensions** no objeto do grupo de medidas.  
  
 Para cada atributo na tupla especificada com granularidade (ou seja, onde o membro na tupla não seja o membro Todos), a coordenada atual para cada atributo é movida da seguinte forma:  
  
-   Os atributos relacionados ao membro de atributo especificado são movidos para o membro que existe com o membro atual.  
  
-   Atributos relacionados ao membro de atributo especificado são movidos para o membro Todos (ou o membro padrão, se a hierarquia não for não agregável).  
  
-   Atributos não relacionados são movidos para o membro Todos (baseado em medida).  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir mostra como a função ValidMeasure pode ser usada para sobrepor o comportamento da propriedade IgnoreUnrelatedDimensions. No cubo Adventure Works, o grupo de medidas Público-Alvo das Vendas tem a propriedade IgnoreUnrelatedDimensions definida para False; como a dimensão Data se junta a esse grupo de medidas na granularidade Trimestre Calendário, significa que a medida Cota de Vendas retornará, por padrão, um valor nulo abaixo de Trimestre Calendário (embora também haja um cálculo no script MDX que aloca valores também ao nível Mês). A função ValidMeasure em uma medida calculada pode ser usada para fazer com que a medida Cota de Vendas comporte-se como se a propriedade IgnoreUnrelatedDimensions estivesse definida como True e forçar a medida Cota de Vendas a exibir o valor do Trimestre Calendário atual.  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 Da mesma forma, a medida Público-Alvo das Vendas não tem relação alguma com a dimensão Promoção e, portanto, abaixo de Todos os Membros de qualquer hierarquia de Promoção, ela retornará um valor nulo. Novamente, esse comportamento pode ser alterado usando ValidMeasure:  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
