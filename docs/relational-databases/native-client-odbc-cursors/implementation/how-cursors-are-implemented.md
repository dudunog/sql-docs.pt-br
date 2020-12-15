---
description: Como os cursores são implementados
title: Como os cursores são implementados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0eaa1db7e0a1de4a893e95e2ca6c6d7c7e7e761f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438665"
---
# <a name="how-cursors-are-implemented"></a>Como os cursores são implementados
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Os aplicativos ODBC controlam o comportamento de um cursor definindo um ou mais atributos de instrução antes de executar uma instrução SQL. ODBC tem dois modos diferentes de especificar as características de um cursor:  
  
-   Tipo de cursor  
  
     Os tipos de cursor são definidos usando o atributo SQL_ATTR_CURSOR_TYPE de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Os tipos de cursor ODBC são de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico. Definir o tipo do cursor era o método original de especificação de cursores no ODBC.  
  
-   Comportamento do cursor  
  
     O comportamento do cursor é definido usando os atributos SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY de **SQLSetStmtAttr**. Esses atributos são modelados nas palavras-chave SCROLL e SENSITIVE definidas para a instrução DECLARE CURSOR com base nos padrões ISO. Essas duas opções ISO foram introduzidas no ODBC versão 3.0.  
  
 As características de um cursor ODBC devem ser especificadas com um desses dois métodos, sendo preferível usar o primeiro, ou seja, tipo do cursor ODBC.  
  
 Além de definir o tipo de um cursor, os aplicativos ODBC também definem outras opções, tais como o número de linhas retornadas em cada extração, opções de simultaneidade e níveis de isolamento da transação. Essas opções podem ser definidas para cursores do tipo ODBC (de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico) ou cursores ISO (rolagem e sensibilidade).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte a várias maneiras de implementar fisicamente os vários tipos de cursores. O driver implementa alguns tipos de cursor usando um conjunto de resultados padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; ele implementa outros como cursores de servidor ou usando a biblioteca de cursores ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando conjuntos de resultados padrão do SQL Server](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
-   [Usando cursores de servidor](../../../relational-databases/native-client-odbc-cursors/implementation/using-server-cursors.md)  
  
-   [Biblioteca de cursores ODBC](../../../relational-databases/native-client-odbc-cursors/implementation/odbc-cursor-library.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
