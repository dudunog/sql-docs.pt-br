---
description: Diagnósticos
title: Diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 918dce41ca1c7e7b43c1a6d25de2c75a83312715
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476708"
---
# <a name="diagnostics"></a>Diagnósticos
As funções no ODBC retornam informações de diagnóstico de duas maneiras. O código de retorno indica o êxito geral ou a falha da função, enquanto os registros de diagnóstico fornecem informações detalhadas sobre a função. Pelo menos um registro de diagnóstico-o registro de cabeçalho-é retornado mesmo que a função tenha sucesso.  
  
 As informações de diagnóstico são usadas em tempo de desenvolvimento para detectar erros de programação, como identificadores inválidos e erros de sintaxe em instruções SQL embutidas em código. Ele é usado em tempo de execução para capturar erros e avisos em tempo de execução, como truncamento de dados, violações de acesso e erros de sintaxe em instruções SQL inseridas pelo usuário.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Usar SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementar SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Exemplos de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
