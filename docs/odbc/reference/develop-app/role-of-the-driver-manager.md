---
description: Função do Gerenciador do Driver
title: Função do Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f974fe6436173b55f39aced45cc38312221cffaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465653"
---
# <a name="role-of-the-driver-manager"></a>Função do Gerenciador do Driver
O Gerenciador de driver determina a ordem final para retornar os registros de status que ele gera. Em particular, ele determina qual registro tem a classificação mais alta e é retornado primeiro. O driver é responsável por ordenar os registros de status que ele gera. Se os registros de status forem postados pelo Gerenciador de driver e pelo driver, o Gerenciador de driver será responsável por ordená-los. Para obter mais informações, consulte [Sequence of status Records](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 O Gerenciador de driver faz o máximo de verificação de erros possível. Isso evita que todos os drivers verifiquem os mesmos erros. Por exemplo, se um argumento de função aceitar um número discreto de valores, como a *operação* em **SQLSetPos**, o Gerenciador de driver verificará se o valor especificado é válido.  
  
 As seções a seguir descrevem os tipos de condições verificadas pelo Gerenciador de driver. Eles não devem ser exaustivas; para obter uma lista completa dos sqlstates que o Gerenciador de driver retorna, consulte a seção "diagnóstico" de cada função; a descrição de cada verificação feita pelo Gerenciador de driver começa com as letras "(DM)". Consulte também as tabelas de transição de estado no [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); os erros mostrados entre parênteses são detectados pelo Gerenciador de driver.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Verificações de valor de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Verificações de transição de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Verificações de erro gerais](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Verificações de aviso e de erro do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
