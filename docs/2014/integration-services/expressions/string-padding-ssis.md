---
title: Preenchimento de cadeia (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a572fd3fc238faabfb80e6b85d42fd887237dc27
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969036"
---
# <a name="string-padding-ssis"></a>Preenchimento de cadeia (SSIS)
  O avaliador de expressão não verifica se uma cadeia de caracteres contém espaços à esquerda e à direita, e não preenche as cadeias de caracteres para que fiquem com o mesmo comprimento antes de compará-las. Se as expressões exigirem preenchimento de cadeia de caracteres, você poderá usar o operador + para concatenar valores de coluna e cadeias de caracteres vazias. Para obter mais informações, consulte [+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](concatenate-ssis-expression.md).  
  
 Por ouro lado, se você quiser remover espaços, o avaliador de expressão fornece as funções LTRIM, RTRIM e TRIM, que removem os espaços à esquerda e/ou à direita. Para obter mais informações, consulte [LTRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md), [RTRIM &#40;Expressão SSIS&#41;](rtrim-ssis-expression.md) e [TRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md).  
  
> [!NOTE]  
>  A função LEN inclui espaços em branco à esquerda e à direita em sua conta.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet
), em pragmaticworks.com  
  
  
