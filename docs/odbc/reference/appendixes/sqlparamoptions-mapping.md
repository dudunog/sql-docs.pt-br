---
description: Mapeamento SQLParamOptions
title: Mapeamento de sqlparamoptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLParamOptions
- SQLParamOptions function [ODBC], mapping
ms.assetid: 57ed65f6-9620-4738-b331-19d2a2b5cae4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a2204921708f6eb2ae7a65925d5c858a0020898
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424899"
---
# <a name="sqlparamoptions-mapping"></a>Mapeamento SQLParamOptions
Quando um aplicativo chama **Sqlparamoptions** por meio de um driver ODBC *3. x* , a chamada  
  
```  
SQLParamOptions(hstmt, crow, piRow);  
```  
  
 será mapeado para duas chamadas de **SQLSetStmtAttr** da seguinte maneira:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, crow, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, piRow, 0);  
```
