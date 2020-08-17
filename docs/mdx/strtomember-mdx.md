---
description: StrToMember (MDX)
title: StrToMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d2d99bb51412a98919d1ab1626c7a86bd86245
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386802"
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)


  Retorna o membro especificado por uma cadeia de caracteres formatada com MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válidos especificando, direta ou indiretamente, um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **StrToMember** retorna o membro especificado na expressão de cadeia de caracteres. A função **StrToMember** normalmente é usada com funções definidas pelo usuário para retornar uma especificação de membro de uma função externa de volta para uma instrução MDX ou quando uma consulta MDX é parametrizada.  
  
-   Quando o sinalizador CONSTRAINED for usado, o nome de membro deverá ser diretamente resolvido para um nome de membro qualificado ou não qualificado. Esse sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma cadeia de caracteres fornecida não for totalmente resolvida para um nome de membro qualificado ou não qualificado, surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOMEMBER foram violadas".  
  
-   Quando o sinalizador de CONSTRAINED não for usado, o membro especificado poderá resolver diretamente um nome de membro ou uma linguagem MDX que resolve um nome.  
  
-   Para entender melhor as diferenças entre conjuntos e membros, consulte Usando expressões de conjuntos e Usando expressões de membros.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a medida valor das vendas do revendedor para o membro Bayern na hierarquia de atributo State-província usando a função **StrToMember** . A cadeia de caracteres especificada forneceu o nome de membro qualificado.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida valor das vendas do revendedor para o membro Bayern usando a função **StrToMember** . Considerando que a cadeia de caracteres de nome de membro forneceu apenas um nome de membro não qualificado, a consulta retorna a primeira instância do membro especificado, que está na hierarquia Geografia do Cliente, na dimensão Cliente, que não faz intersecção com Vendas do Revendedor. As práticas recomendadas ditam que se especifique o nome qualificado para assegurar resultados esperados.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida valor das vendas do revendedor para o membro Bayern na hierarquia de atributo State-província usando a função **StrToMember** . A cadeia de caracteres de nome de membro fornecida resolve um nome de membro qualificado.  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna um erro devido ao sinalizador CONSTRAINED. Enquanto a cadeia de caracteres de nome de membro fornecida contém uma expressão de membro MDX válida, que resolve um nome de membro qualificado, o sinalizador CONSTRAINED exige nomes de membros qualificados ou não qualificados na cadeia de caracteres de nome de membro.  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
