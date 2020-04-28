---
title: Desconectando de uma fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de6722994ca31af3fef9a359f4bb01b5f1fc64c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305489"
---
# <a name="disconnecting-from-a-data-source"></a>Desconectando uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando um aplicativo termina de usar uma fonte de dados, ele chama **SQLDisconnect**. O **SQLDisconnect** libera Todas as instruções que são alocadas na conexão e desconecta o driver da fonte de dados. Após a desconexão, o aplicativo pode chamar [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de conexão. Antes de sair, um aplicativo também chama **SQLFreeHandle** para liberar o identificador do ambiente.  
  
 Depois de desconectar, um aplicativo pode reutilizar o identificador de conexão alocado para se conectar a uma outra fonte de dados ou para reconectar-se à mesma fonte de dados. A decisão de permanecer conectado em vez de desconectar e reconectar posteriormente exige que o criador do aplicativo considere os custos relativos de cada opção. Conectar-se a uma fonte de dados e permanecer conectado podem ser relativamente caro, dependendo do meio de conexão. Ao fazer uma compensação, o aplicativo deve também fazer suposições sobre a probabilidade e o tempo das operações adicionais na mesma fonte de dados. Talvez o aplicativo também precise usar mais de uma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Comunicando-se com SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
