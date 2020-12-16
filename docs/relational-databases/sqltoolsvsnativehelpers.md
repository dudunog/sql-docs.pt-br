---
description: SqlToolsVSNativeHelpers
title: SqlToolsVSNativeHelpers | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3539245b59399d8fc6bcebea6bd97f10df73dbba
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461807"
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
  Biblioteca que oferece suporte à funcionalidade do SQL Server no Visual Studio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano **True** se o ponto de entrada da DLL for inicializado corretamente; do contrário, será **False**.  
  
## <a name="see-also"></a>Consulte Também  
 [FrameWindowVisible](../relational-databases/sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  
