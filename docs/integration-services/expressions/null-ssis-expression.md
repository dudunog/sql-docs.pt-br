---
title: NULL (expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 574c846d2fb002fe317ddc8e3000aeabbb5cf082
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921367"
---
# <a name="null-ssis-expression"></a>NULL (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Retorna um valor nulo de um tipo de dados solicitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>Argumentos  
 *typespec*  
 É um tipo de dados válido. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Qualquer tipo de dados válido com um valor nulo.  
  
## <a name="remarks"></a>Comentários  
 NULL retornará um resultado nulo se o argumento for nulo.  
  
 Os parâmetros são exigidos para solicitar um valor nulo para alguns tipos de dados. A tabela a seguir lista esses tipos de dados e seus parâmetros.  
  
|Tipo de dados|Parâmetro|Exemplo|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) converte 30 caracteres para o tipo de dados de DT_STR usando a página de código 1252.|  
|DT_WSTR|*charcount*|(DT_WSTR,20) converte 20 caracteres para o tipo de dados de DT_WSTR.|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) converte 50 bytes para o tipo de dados de DT_BYTES.|  
|DT_DECIMAL|*scale*|(DT_DECIMAL,2) converte um valor numérico para o tipo de dados DT_DECIMAL usando uma escala de 2.|  
|DT_NUMERIC|*precisão*<br /><br /> *scale*|(DT_NUMERIC,10,3) converte um valor numérico para o tipo de dados DT_NUMERIC usando uma precisão de 10 e uma escala de 3.|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) converte um valor para o tipo de dados DT_TEXT usando a página de código 1252.|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esses exemplos retornam o valor nulo dos tipos de dados: DT_STR, DT_DATE e DT_BOOL.  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ISNULL &#40;Expressão SSIS&#41;](../../integration-services/expressions/isnull-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
