---
title: Sintaxe de comando | Microsoft Docs
description: Procedimentos armazenados e sintaxe do comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 15d6d221c9e3435a3ba4c3f58c7d6b6e55314f29
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68016126"
---
# <a name="command-syntax"></a>Sintaxe de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server reconhece a sintaxe de comando especificada pela macro DBGUID_SQL. Para o Driver do OLE DB para SQL Server, o especificador indica que uma mistura do ODBC SQL, ISO e [!INCLUDE[tsql](../../../includes/tsql-md.md)] é uma sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função LOWER de cadeia de caracteres ISO executa a mesma operação, assim a seguinte instrução SQL é uma equivalente ISO para a instrução ODBC apresentada acima:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 O OLE DB Driver for SQL Server processa uma das duas formas da instrução com êxito quando especificada como texto de um comando.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 Ao executar um procedimento armazenado do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um comando do OLE DB Driver for SQL Server, use a sequência de escape CALL do ODBC no texto do comando. Em seguida, o OLE DB Driver for SQL Server usa o mecanismo de chamada de procedimento remoto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para otimizar o processamento do comando. Por exemplo, a seguinte instrução SQL do ODBC é o texto de comando preferido à forma do [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
