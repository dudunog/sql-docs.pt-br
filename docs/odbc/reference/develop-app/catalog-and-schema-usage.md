---
description: Catálogo e o uso do esquema
title: Uso de catálogo e esquema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2506810c477e9d75e1d3b38f38185d22edf9d010
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494686"
---
# <a name="catalog-and-schema-usage"></a>Catálogo e o uso do esquema
As fontes de dados não oferecem necessariamente suporte a nomes de catálogo e de esquema como identificadores de nome de objeto em todas as instruções SQL. As fontes de dados podem dar suporte a nomes de catálogo e de esquema em uma ou mais das seguintes classes de instruções SQL: instruções DML (linguagem de manipulação de dados), chamadas de procedimento, instruções de definição de tabela, instruções de definição de índice e instruções de definição de privilégio. Para determinar as classes de instruções SQL nas quais os nomes de catálogo e de esquema podem ser usados, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
