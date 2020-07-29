---
title: Consultas de parâmetros
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- parameter queries [SQL Server]
ms.assetid: 4897c41a-324a-47b8-a30b-cbc9e9e19a8b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: f0cfe484f628040bf419738f79e6500cc6911f83
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003234"
---
# <a name="parameter-queries-visual-database-tools"></a>Consultas de parâmetros (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Em alguns casos, talvez você queira criar uma consulta que possa ser utilizada muitas vezes, mas com um valor diferente a cada vez. Por exemplo, pode ser que você execute com frequência uma consulta para localizar todos os `title_ids` escritos por um autor. Você pode executar a mesma consulta para cada solicitação, exceto se a ID ou o nome do autor forem diferentes.  
  
Você utilizará parâmetros na consulta para criar uma consulta que possa ter valores diferentes a cada momento. Um parâmetro é um espaço reservado para um valor fornecido quando a consulta é executada. Uma instrução SQL com um parâmetro pode se parecer com a seguinte, em que "?" representa o parâmetro da ID do autor:  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
## <a name="where-you-can-use-parameters"></a>Onde você pode utilizar parâmetros  
Você pode usar parâmetros como espaços reservados para valores literais – tanto para valores de texto quanto numéricos. Geralmente, os parâmetros são utilizados como espaços reservados em critérios de pesquisa para linhas individuais ou para grupos (ou seja, nas cláusulas WHERE ou HAVING de uma instrução SQL).  
  
Você pode utilizar parâmetros como espaços reservados em expressões. Por exemplo, você pode querer calcular preços com desconto fornecendo um valor de desconto diferente a cada vez que executar uma consulta. Para fazer isso, você poderá especificar a seguinte expressão:  
  
```  
(price * ?)  
```  
  
## <a name="specifying-unnamed-and-named-parameters"></a>Especificando parâmetros com e sem-nome  
Você pode especificar dois tipos de parâmetros: com e sem-nome. Um parâmetro sem nome é um ponto de interrogação (?) que você coloca em qualquer lugar na consulta em que queira solicitar ou substituir um valor literal. Por exemplo, se você utilizar um parâmetro sem nome para pesquisar a ID de um autor na tabela `titleauthor` , a instrução resultante no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) poderá se parecer com:  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
Quando você executa uma consulta no [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md), a caixa de diálogo [Parâmetros da Consulta](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) é exibida com "?" como o nome do parâmetro.  
  
Como alternativa, você pode atribuir um nome a um parâmetro. Os parâmetros com nome são muito úteis se você tiver diversos parâmetros em uma consulta. Por exemplo, se você utilizar um parâmetro com nome para pesquisar o nome e o sobrenome de um autor na tabela `authors` , a instrução resultante no painel SQL poderia se parecer com:  
  
```  
SELECT au_id  
FROM authors  
WHERE au_fname = %first name% AND  
      au_lname = %last name%  
```  
  
> [!TIP]  
> Você deve definir caracteres de prefixo e de sufixo antes de criar uma consulta de parâmetro com nome.  
  
Quando você executa uma consulta no Designer de Consulta e Exibição, a caixa de diálogo [Parâmetros de Consulta](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) é exibida com uma lista de parâmetros com nome.  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
