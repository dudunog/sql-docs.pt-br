---
title: YEAR (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c3583baedb1766944a89b9f4491c53a94a17f3fa
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297311"
---
# <a name="year-ssis-expression"></a>YEAR (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna um inteiro que representa o ano da parte da data.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma data em qualquer formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 YEAR retornará um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  A expressão não é validada quando um literal de data é convertido explicitamente em um destes tipos de dados de data: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 A função YEAR é mais resumida, mas equivale a usar a função DATEPART ("Ano", data).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o número do ano em um literal de data. Se a data estiver no formato mm/dd/aaaa, este exemplo retornará "2002".  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este exemplo retorna o inteiro que representa o ano na coluna **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 Este exemplo retorna o inteiro que representa o ano da data atual.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
