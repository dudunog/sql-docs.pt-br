---
description: Função do driver
title: Função do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: afd8f058b12b30140bb193ded7a23e8daf365865
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465642"
---
# <a name="role-of-the-driver"></a>Função do driver
O driver verifica todos os erros e avisos não verificados pelo Gerenciador de driver e os registros de status de pedidos que ele gera. (Um ODBC 2. o driver *x* não ordena registros de status.) Isso inclui erros e avisos no truncamento de dados, na conversão de dados, na sintaxe e em algumas transições de estado. O driver também pode verificar erros e avisos parcialmente verificados pelo Gerenciador de driver. Por exemplo, embora o Gerenciador de driver Verifique se o valor de *operação* em **SQLSetPos** é legal, o driver deve verificar se há suporte para ele.  
  
 O driver também mapeia *erros nativos* , ou seja, erros retornados pela fonte de dados-para sqlstates. Por exemplo, o driver pode mapear vários erros nativos diferentes para sintaxe SQL ilegal para SQLSTATE 42000 (erro de sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. A documentação do driver deve mostrar como os erros e avisos são mapeados da fonte de dados para argumentos em **SQLGetDiagRec** e **SQLGetDiagField**.
