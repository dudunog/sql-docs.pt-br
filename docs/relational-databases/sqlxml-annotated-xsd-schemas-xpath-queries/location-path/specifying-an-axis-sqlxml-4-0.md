---
title: Especificando um eixo (SQLXML)
description: Saiba como especificar um eixo em uma consulta XPath do SQLXML 4,0 especifica a relação de árvore entre os nós selecionados pela etapa local e o nó de contexto.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03c0fff271ef3774116eb9c97025b1f602f7852c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431154"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Especificando um eixo (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
    
-   O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Há suporte para os seguintes eixos:  **filho**  
  
     Contém o filho do nó de contexto.  
  
     A seguinte expressão XPath (caminho de localização) seleciona a partir do nó de contexto atual todos os **\<Customer>** filhos:  
  
    ```  
    child::Customer  
    ```  
  
     Na consulta XPath a seguir, `child` é o eixo. `Customer` é o teste de nó.  
  
-   **parent**  
  
     Contém o pai do nó de contexto.  
  
     A expressão XPath a seguir seleciona todos os **\<Customer>** pais dos **\<Order>** filhos:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Isso corresponde à especificação de `child::Customer`. Nesta consulta XPath, `child` e `parent` são os eixos. `Customer` e `Order` são os testes de nó.  
  
-   **Attribute**  
  
     Contém o atributo do nó de contexto.  
  
     A expressão XPath a seguir seleciona o atributo **CustomerID** do nó de contexto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **auto-restauração**  
  
     Contém o próprio nó de contexto.  
  
     A expressão XPath a seguir selecionará o nó atual se ele for o **\<Order>** nó:  
  
    ```  
    self::Order  
    ```  
  
     Nesta consulta XPath, `self` é o eixo e `Order` é o teste de nó.  
  
  
