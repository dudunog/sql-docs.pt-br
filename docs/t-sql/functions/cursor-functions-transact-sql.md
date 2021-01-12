---
description: funções de cursor (Transact-SQL)
title: Funções de cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3433a39caeb0a1e951eba18ccdd3d1658c108252
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98087616"
---
# <a name="cursor-functions-transact-sql"></a>funções de cursor (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Estas funções escalares retornam informações sobre cursores:
  
- [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)
- [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)
- [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)
  
Todas as funções de cursor são não determinísticas. Em outras palavras, essas funções nem sempre retornam os mesmos resultados sempre que são executadas, mesmo com o mesmo conjunto de valores de entrada. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo de funções.
  
## <a name="see-also"></a>Confira também

[Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
