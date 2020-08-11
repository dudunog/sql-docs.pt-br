---
title: Função Last (Construtor de Relatórios) | Microsoft Docs
description: A função Last retornará o valor final em um conjunto de dados depois que toda a classificação e filtragem tiverem sido aplicadas no escopo especificado no Construtor de Relatórios.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 123b78a0-d6c9-4f78-b0e7-73b21854a250
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 68f4341c6f747ae58f11ce0c210a7ef4fac78997
ms.sourcegitcommit: f898aa83561e94626024916932568ab05e73b656
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/27/2020
ms.locfileid: "84012614"
---
# <a name="report-builder-functions---last-function"></a>Funções do Construtor de Relatórios – Função Last
  Retorna o último valor no escopo fornecido da expressão especificada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Last(expression, scope)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *expressão*  
 (**Variant** ou **Binary**) A expressão na qual a agregação será executada, por exemplo, `=Fields!Fieldname.Value`.  
  
 *escopo*  
 (**String**) (Opcional) O nome de um conjunto de dados, região de dados ou grupo que contém os itens do relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## <a name="return-type"></a>Tipo de retorno  
 Determinado pelo tipo de expressão.  
  
## <a name="remarks"></a>Comentários  
 A função **Last** retorna o valor final em um conjunto de dados depois que toda a classificação e filtragem tiverem sido aplicadas no escopo especificado.  
  
 A função **Last** não pode ser usada em expressões de filtro de grupo com qualquer coisa, exceto o escopo atual (padrão).  
  
 É possível usar também a função **Last** em um cabeçalho de página para retornar o último valor da coleção de **ReportItems** para uma página de modo a produzir cabeçalhos em estilo de dicionário que exibem a primeira e a última entradas em uma página.  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expression* não deve conter a função **First**, **Last**, **Previous**ou **RunningValue** .  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir retorna o número do último produto no grupo `Category` de uma região de dados.  
  
```  
=Last(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
