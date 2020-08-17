---
description: Manipulação de dados MDX – CLEAR CALCULATIONS
title: Instrução CLEAR CALCULAtions (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f3fc9d29630f3f69b994c2b4e7cf809b6b9efd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387000"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulação de dados MDX – CLEAR CALCULATIONS


  Remove todos os cálculos do cubo e retorna o cubo para a análise de cálculo 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Uma expressão de cubo da linguagem MDX válida.  
  
## <a name="remarks"></a>Comentários  
 A cláusula **from** pode ser omitida quando o contexto do cubo é conhecido, como em um script MDX.  
  
> [!NOTE]  
>  Essa instrução só pode ser executada por um administrador de banco de dados ou servidor ou por um membro de uma função que tenha acesso aos dados de origem no cubo (ou seja, ReadSourceData=true)  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de manipulação de dados MDX &#40;&#41;MDX ](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
