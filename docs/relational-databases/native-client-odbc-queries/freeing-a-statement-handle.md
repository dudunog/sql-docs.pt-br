---
title: Liberando um identificador de instrução | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e954773f85afc434d1e5bd18f7ffb76e28a1438
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297883"
---
# <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  É mais eficiente reutilizar identificadores de instrução do que eliminá-los e alocar novos. Antes de executar uma nova instrução SQL em um identificador de instrução, os aplicativos deverão verificar se as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, os parâmetros e os conjuntos de resultados para a instrução SQL antiga devem ser desassociados chamando [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com as opções SQL_RESET_PARAMS e SQL_UNBIND e, em seguida, reassociar para a nova instrução SQL.  
  
 Quando o aplicativo termina de usar a instrução, ele chama [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar a instrução. Observe que **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
