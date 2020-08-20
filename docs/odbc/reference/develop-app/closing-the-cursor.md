---
description: Fechar o cursor
title: Fechando o cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd9465f0fc076a4f41dd8bf4cb3463ce5a47de84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461567"
---
# <a name="closing-the-cursor"></a>Fechar o cursor
Quando um aplicativo termina de usar um cursor, ele chama **SQLCloseCursor** para fechar o cursor. Por exemplo:   
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Até que o aplicativo feche o cursor, a instrução na qual o cursor está aberto não pode ser usada para a maioria das outras operações, como a execução de outra instrução SQL. Para obter uma lista completa das funções que podem ser chamadas enquanto um cursor estiver aberto, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, e não **SQLCancel**.  
  
 Os cursores permanecem abertos até que sejam explicitamente fechados, exceto quando uma transação é confirmada ou revertida; nesse caso, algumas fontes de dados fecham o cursor. Em particular, atingindo o final do conjunto de resultados, quando **SQLFetch** retorna SQL_NO_DATA, o não fecha um cursor. Até mesmo cursores em conjuntos de resultados vazios (conjuntos de resultados criados quando uma instrução executada com êxito, mas que não retornaram linhas) devem ser fechados explicitamente.
