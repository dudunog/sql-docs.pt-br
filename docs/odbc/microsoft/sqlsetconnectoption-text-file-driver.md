---
title: SQLSetConnectOption (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6442134086ea6fe15b393b87d6c80019a076be2a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306131"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O SQL_ACCESS_MODE fOption pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impedirá atualizações se SQL_ACCESS_MODE estiver definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|O driver de texto só dá suporte a SQL_AUTOCOMMIT ser definido como ON (o estado padrão), porque eles não dão suporte a transações.|  
|SQL_CURRENT_QUALIFIER| Com suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE| Com suporte.|  
|SQL_OPT_TRACEFILE| Com suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|Sem suporte.|
