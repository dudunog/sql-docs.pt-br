---
title: Criando medidas em MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
author: minewiskan
ms.author: owend
ms.openlocfilehash: ac49d37f11584bfbc5d372241056da39e7dd8c93
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546498"
---
# <a name="building-measures-in-mdx"></a>Compilando medidas em MDX
  Nas expressões MDX, uma medida é uma expressão DAX nomeada que é resolvida pelo cálculo da expressão para retornar um valor em um Modelo de Tabela. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar medidas em uma consulta MDX proporciona uma grande capacidade de manipulação de dados de tabela.  
  
> [!WARNING]  
>  As medidas podem ser definidas apenas em modelos de tabela; se o seu banco de dados estiver definido no modo multidimensional, a criação de uma medida gerará um erro  
  
 Para criar uma medida que seja definida como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Em seguida, você pode usar a medida em uma instrução MDX SELECT. Usando essa abordagem, o membro calculado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT. No entanto, em MDX você referencia a medida de uma forma diferente da adotada nas expressões DAX; para referenciar a medida você a denomina como membro da dimensão [Measures], consulte o seguinte exemplo de MDX:  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 Isso retornará os dados seguintes quando executado:  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Referência de função MDX &#40;&#41;MDX](/sql/mdx/mdx-function-reference-mdx)   
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
