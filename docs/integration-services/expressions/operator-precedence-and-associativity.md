---
description: Precedência de operador e capacidade de associação
title: Precedência de operador e capacidade de associação | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cda01c12856bff3e28b06c9cfddccb368e6a3e6b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477479"
---
# <a name="operator-precedence-and-associativity"></a>Precedência de operador e capacidade de associação

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Cada operador no conjunto de operadores que o avaliador de expressão aceita tem uma precedência designada na hierarquia de precedência e inclui uma direção na qual ele será avaliado. A direção de avaliação para um operador é a capacidade de associação do operador. Os operadores com maior precedência são avaliados antes dos operadores com menor precedência. Se uma expressão complexa tiver vários operadores, a precedência de operador determina a ordem na qual as operações são executadas. A ordem de execução pode afetar o valor resultante significativamente. Alguns operadores têm precedência igual. Se uma expressão contiver vários operadores de precedência igual, os operadores serão avaliados de forma direcional, da esquerda para a direita ou da direita para a esquerda.  
  
 A tabela a seguir lista a precedência de operadores na ordem de cima para baixo. Os operadores ao mesmo nível têm precedência igual.  
  
|Símbolo do operador|Tipo de operação|Capacidade de associação|  
|---------------------|-----------------------|-------------------|  
|( )|Expression|Da esquerda para a direita|  
|-, !, ~|Unário|Da direita para a esquerda|  
|conversões|Unário|Da direita para a esquerda|  
|*, / ,%|Multiplicativo|Da esquerda para a direita|  
|+, -|Aditiva|Da esquerda para a direita|  
|\<, >, \<=, >=|Relacional|Da esquerda para a direita|  
|==, !=|Igualitário|Da esquerda para a direita|  
|&|AND bit a bit|Da esquerda para a direita|  
|^|OR exclusivo bit a bit|Da esquerda para a direita|  
|&#124;|OR inclusivo bit a bit|Da esquerda para a direita|  
|&&|AND lógico|Da esquerda para a direita|  
|&#124;&#124;|OR lógico|Da esquerda para a direita|  
|? :|Expressões condicionais|Da direita para a esquerda|  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
