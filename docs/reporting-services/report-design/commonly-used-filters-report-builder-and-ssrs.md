---
title: Os filtros mais usados (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- multivalued parameters [Reporting Services]
- single-valued parameters [Reporting Services]
- parameters [Reporting Services], multivalued
- valid values [Reporting Services]
ms.assetid: cb70d0cd-707b-4de5-b39f-e4eb57d316aa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d0a096fd9dcb292f1a71b74aaf853abcbd7c02ae
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082313"
---
# <a name="commonly-used-filters-report-builder-and-ssrs"></a>Filtros comumente usados (Construtor de Relatórios e SSRS)
  Para criar um filtro, é necessário especificar uma ou mais equações de filtro. As equações de filtro incluem uma expressão, um tipo de dados, um operador e um valor. Este tópico traz exemplos de filtros que são utilizados com frequência.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Exemplos de filtro  
 A tabela a seguir mostra exemplo de equações de filtro que usam diferentes tipos de dados e operadores. O escopo da comparação é determinado pelo item de relatório para o qual é definido um filtro. Por exemplo, no caso de um filtro definido em um conjunto de dados, **TOP % 10** representa os principais 10% de valores do conjunto de dados; no caso de um filtro definido em um grupo, **TOP % 10** são os principais 10% de valores do grupo.  
  
|Expressão simples|Tipo de Dados|Operador|Valor|DESCRIÇÃO|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Inteiro**|**>**|`7`|Inclui valores de dados maiores que 7.|  
|`[SUM(Quantity)]`|**Inteiro**|**TOP N**|`10`|Inclui os 10 principais valores de dados.|  
|`[SUM(Quantity)]`|**Inteiro**|**TOP %**|`20`|Inclui os principais 20% de valores de dados.|  
|`[Sales]`|**Texto**|**>**|`=CDec(100)`|Inclui todos os valores do tipo System.Decimal (tipos de dados “money” do SQL) maiores que $100.|  
|`[OrderDate]`|**DateTime**|**>**|`2088-01-01`|Inclui todas as datas, desde 1º de janeiro de 2008 até a presente data.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Inclui as datas de 1o. de janeiro de 2008 até, e incluindo, 1º de fevereiro de 2008.|  
|`[Territory]`|**Texto**|**LIKE**|`*east`|Todos os nomes de território que terminam com "leste".|  
|`[Territory]`|**Texto**|**LIKE**|`%o%th*`|Todos os nomes de território que incluem Norte e Sul no início do nome.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Texto**|**IN**|`B, C, T`|Todos os valores de subcategorias que começam com as letras B, C ou T.|  
  
## <a name="examples-with-report-parameters"></a>Exemplos com parâmetros de relatório  
 A tabela a seguir contém exemplos de expressão de filtro que inclui uma referência de parâmetro de um só valor ou multivalor.  
  
|Tipo de parâmetro|Expressão (filtro)|Operador|Valor|Tipo de Dados|  
|--------------------|---------------------------|--------------|-----------|---------------|  
|Um único valor|`[EmployeeID]`|=|`[@EmployeeID]`|Integer|  
|Multivalor|`[EmployeeID]`|IN|`[@EmployeeID]`|Integer|  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)  
  
  
