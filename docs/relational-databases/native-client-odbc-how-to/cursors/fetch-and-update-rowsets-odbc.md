---
description: Buscar e atualizar conjuntos de linhas (ODBC)
title: Buscar e atualizar conjuntos de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5eaa9a150589cbdf41a41d3528b2b49b00cd7c9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467757"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Buscar e atualizar conjuntos de linhas (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>Para buscar e atualizar conjuntos de linhas  
  
1.  Opcionalmente, chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com SQL_ROW_ARRAY_SIZE para alterar o número de linhas (R) no conjunto de linhas.  
  
2.  Chame [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) ou [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) para obter um conjunto de linhas.  
  
3.  Se forem usadas colunas associadas, use os valores e comprimentos de dados disponíveis agora nos buffers de coluna associada para o conjunto de linhas.  
  
     Se forem usadas colunas desassociadas, para cada chamada de linha [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) com SQL_POSITION para definir a posição do cursor; em seguida, para cada coluna desassociada:  
  
    -   Chame [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados de colunas desassociadas após a última coluna associada do conjunto de linhas. As chamadas para [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) devem estar na ordem de aumento do número da coluna.  
  
    -   Chame [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Configure quaisquer colunas de imagem ou texto de dados em execução.  
  
5.  Chame [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) ou [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) para definir a posição do cursor, atualizar, atualizar, excluir ou Adicionar linha (s) no conjunto de linhas.  
  
     Se as colunas de imagem ou texto de dados em execução forem usadas para uma operação de atualização ou adição, lide com elas.  
  
6.  Opcionalmente, execute uma instrução UPDATE ou DELETE posicionada, especificando o nome do cursor (disponível em [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) e usando um identificador de instrução diferente na mesma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre o uso de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
