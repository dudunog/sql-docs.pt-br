---
description: Definição de dados MDX – CREATE MEASURE
title: Instrução CREATE MEASURE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: af9ff1465c23231637cac636bb63702e79cf054c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098329"
---
# <a name="mdx-data-definition---create-measure"></a>Definição de dados MDX – CREATE MEASURE


  Cria uma medida em um Modelo de Tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Table_Name*  
 Um literal de cadeia de caracteres válido que fornece o nome da tabela onde a medida será criada.  
  
 *Measure_Name*  
 Um literal de cadeia de caracteres válido que fornece um nome de medida.  
  
 *DAX_Expression*  
 Uma expressão DAX válida que retorna um único valor escalar.  
  
## <a name="remarks"></a>Comentários  
 O *MEASURE_NAME*  deve ser colocado entre parênteses.  
  
 A instrução CREATE MEASURE só pode ser usada dentro de uma definição de script MDX; consulte o [elemento MdxScript &#40;ASSL&#41;](/analysis-services/assl/objects/mdxscript-element-assl).  
  
 Também é possível definir um membro calculado para ser usado por uma consulta única. Para definir um membro calculado limitado a uma consulta única, use a cláusula WITH na instrução SELECT. Para obter mais informações, consulte [Building Measures in MDX](/analysis-services/multidimensional-models/mdx/mdx-building-measures).  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
