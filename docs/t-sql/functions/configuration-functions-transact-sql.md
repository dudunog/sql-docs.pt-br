---
description: Funções de configuração (Transact-SQL)
title: Funções de configuração (Transact-SQL) | Microsoft Docs
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
- functions [SQL Server], configuration
- configuration options [SQL Server], functions
- current configuration information
- configuration functions [SQL Server]
ms.assetid: 066f15e7-3406-437e-93c4-3f247c529169
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 904e63d757f71c442e829e68e42d111cc3452186
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459812"
---
# <a name="configuration-functions-transact-sql"></a>Funções de configuração (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essas funções escalares retornam informações sobre as definições de opção de configuração atuais:
  
- [@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)
- [@@DBTS](../../t-sql/functions/dbts-transact-sql.md)
- [@@LANGID](../../t-sql/functions/langid-transact-sql.md)
- [@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)
- [@@LOCK_TIMEOUT](../../t-sql/functions/lock-timeout-transact-sql.md)
- [@@MAX_CONNECTIONS](../../t-sql/functions/max-connections-transact-sql.md)
- [@@MAX_PRECISION](../../t-sql/functions/max-precision-transact-sql.md)
- [@@NESTLEVEL](../../t-sql/functions/nestlevel-transact-sql.md)
- [@@OPTIONS](../../t-sql/functions/options-transact-sql.md)
- [@@REMSERVER](../../t-sql/functions/remserver-transact-sql.md)
- [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)
- [@@SERVICENAME](../../t-sql/functions/servicename-transact-sql.md)
- [@@SPID](../../t-sql/functions/spid-transact-sql.md)
- [@@TEXTSIZE](../../t-sql/functions/textsize-transact-sql.md)
- [@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md)

Todas as funções de configuração operam de modo não determinístico. Em outras palavras, essas funções nem sempre retornam os mesmos resultados a cada chamada, mesmo com o mesmo conjunto de valores de entrada. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo de funções.
  
## <a name="see-also"></a>Confira também

[Funções &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
