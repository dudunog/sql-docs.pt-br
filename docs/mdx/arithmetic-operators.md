---
title: Operadores aritméticos | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1898f3e9807d2ea4f80f99e9a7ef27e672d58a18
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017078"
---
# <a name="arithmetic-operators"></a>Operadores aritméticos


  Use operadores aritméticos em linguagem MDX para qualquer cálculo aritmético, incluindo adição, subtração, multiplicação e divisão.  
  
 O MDX oferece suporte para os operadores aritméticos listados na tabela a seguir.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[+ (Somar)](../mdx/add-mdx.md)|Soma dois números.|  
|[/ (dividir)](../mdx/divide-mdx-operator-reference.md)|Divide um número pelo outro.|  
|[* (Multiplicar)](../mdx/multiply-mdx.md)|Multiplica dois números.|  
|[-(Subtrair)](../mdx/subtract-mdx.md)|Subtrai dois números.|  
|^ (Potência)|Eleva um número pelo outro.|  
  
> [!NOTE]  
>  A linguagem MDX não inclui uma função para obter a raiz quadrada de um número. Para obter a raiz quadrada de um número, eleve-o à potência de 0,5 usando o operador ^.  
  
## <a name="order-of-precedence"></a>Ordem de Precedência  
 As regras a seguir determinam a ordem de prioridade dos operadores aritméticos em uma expressão MDX:  
  
-   Quando houver mais de um operador aritmético em uma expressão, o MDX efetua a multiplicação e a divisão primeiramente, seguidas da subtração e da adição.  
  
-   Quando todos os operadores aritméticos em uma expressão têm o mesmo nível de precedência, a ordem de execução é da esquerda para a direita.  
  
-   Expressões entre parênteses têm precedência sobre todas as outras operações.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
