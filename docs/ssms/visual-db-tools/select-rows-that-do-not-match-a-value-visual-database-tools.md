---
title: Selecionar linhas que não correspondem a um valor
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: ba594307277060abd6ddedb9dd7fda7c1a8bebee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255089"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>Selecionar linhas que não correspondem a um valor (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para localizar linhas que não correspondem a um valor, use o operador NOT.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>Para localizar linhas que não correspondem a um valor  
  
1.  Se você ainda não o fez, adicione as colunas ou expressões que pretende usar nos critérios de pesquisa do [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md).  
  
2.  Localize a linha que contém a coluna de dados ou expressão a ser pesquisada e, em seguida, na coluna de grade **Filtro** , digite o operador NOT seguido de um valor de pesquisa.  
  
Por exemplo, para localizar todas as linhas em uma tabela de `products` em que os valores da coluna de código do produto começam com um caractere diferente de "A", você pode digitar um critério de pesquisa como o seguinte:  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>Consulte Também  
[Regras para inserir valores de pesquisa](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar critérios de pesquisa](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
