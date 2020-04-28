---
title: Especificando um caminho de local (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5e2668da10e41e997cc4d37760d79e4b66dae215
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75245588"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Especificando um caminho para o local (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  São especificadas consultas XPath no formato de uma expressão. Há vários tipos de expressões. Um caminho de local é uma expressão que seleciona um conjunto de nós relativos ao nó de contexto. O resultado de avaliar um caminho de local é um conjunto de nós.  
  
## <a name="types-of-location-paths"></a>Tipos de caminhos de local  
 Um caminho de local pode ter um destes formatos:  
  
-   **Caminho de local absoluto**  
  
     Um caminho de local absoluto inicia no nó raiz do documento. Ele é formado por barra (/) opcionalmente seguida por um caminho de local relativo. A barra (/) seleciona o nó raiz do documento.  
  
-   **Caminho de local relativo**  
  
     Um caminho de local relativo inicia no nó de contexto no documento. Um caminho de local consiste em uma sequência de uma ou mais etapas de local separada por uma barra (/). Cada etapa seleciona um conjunto de nós relativo ao nó de contexto. A sequência inicial de etapas seleciona um conjunto de nós relativo a um nó de contexto. Cada nó nesse conjunto é usado como um nó de contexto para a etapa seguinte. São unidos os conjuntos de nós identificados por esta etapa. Por exemplo, **Child:: ordem/filho:: OrderDetail** seleciona o ** \<** elemento de>de OrderDetail dos filhos do elemento ** \<Order>** do nó de contexto.  
  
    > [!NOTE]  
    >  Na implementação de XPath do SQLXML 4.0, todas as consultas XPath começam no contexto raiz, mesmo que o XPath não seja explicitamente absoluto. Por exemplo, uma consulta XPath que comece com "Customer" é tratada como "/Customer". No cliente de consulta XPath **[pedido]**, o cliente começa no contexto raiz, mas a ordem começa no contexto do cliente. Para obter mais informações, consulte [introdução ao uso de consultas XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Etapas de local  
 Um caminho de local (absoluto ou relativo) é composto por etapas de local que contêm três partes:  
  
-   **Axis**  
  
     O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Há suporte para os eixos **pai**, **filho**, **atributo**e **Self** . Se um eixo **filho** for especificado no caminho do local, todos os nós selecionados pela consulta serão os filhos do nó de contexto. Se um eixo **pai** for especificado, o nó selecionado será o nó pai do nó de contexto. Se um eixo de **atributo** for especificado, os nós selecionados serão os atributos do nó de contexto.  
  
-   **Teste de nó**  
  
     Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Cada eixo (**filho**, **pai**, **atributo**e **Self**) tem um tipo de nó principal. Para o eixo de **atributo** , o tipo de nó principal é ** \<>de atributo **. Para os eixos **pai**, **filho**e **Self** , o tipo de nó principal é ** \<>de elemento **.  
  
     Por exemplo, se o caminho do local especificar **Child:: Customer**, os ** \<** filhos do elemento>do cliente do nó de contexto serão selecionados. Como o eixo **filho** tem ** \<>de elemento** como o tipo de nó principal, o teste de nó, Customer, será true se Customer for um ** \<elemento>** node.  
  
-   **Predicados da seleção (zero ou mais)**  
  
     Um predicado filtra um conjunto de nós em relação a um eixo. A especificação de predicados de seleção em uma expressão XPath é semelhante à especificação de uma cláusula WHERE em uma instrução SELECT. O predicado é especificado entre colchetes. A aplicação do teste especificado nos predicados de seleção filtra os nós retornados pelo teste de nó. Para cada nó no conjunto de nós a ser filtrado, a expressão de predicado é avaliada com esse nó como o nó de contexto, com o número de nós no conjunto de nós como o tamanho do contexto. Se a expressão de predicado for avaliada como TRUE para esse nó, o nó será incluído no conjunto de nós resultante.  
  
     A sintaxe de uma etapa de local é o nome do eixo e o teste de nó separados por dois-pontos duplos (::), seguidos por zero ou mais expressões entre colchetes. Por exemplo, a expressão XPath (caminho do local) **Child:: Customer@CustomerID[= ' ALFKI ']** seleciona todos os ** \<** elementos filho do cliente>do nó de contexto. Em seguida, o teste no predicado é aplicado ao conjunto de nós, que retorna ** \<** somente os nós do elemento de>do cliente com o valor de atributo ' ALFKI ' para seu atributo **CustomerID** .  
  
## <a name="in-this-section"></a>Nesta seção  
 [Especificando um eixo &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 Fornece exemplos de especificação de um eixo.  
  
 [Especificar um teste de nó no caminho do local &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Fornece exemplos de especificação de um teste de nó.  
  
 [Especificar predicados de seleção no caminho do local &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Fornece exemplos de especificação de predicados de seleção.  
  
  
