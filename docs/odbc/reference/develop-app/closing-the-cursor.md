---
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
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299136"
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
