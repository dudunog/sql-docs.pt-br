---
description: Mapeamento SQLGetConnectOption
title: Mapeamento de SQLGetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbb8578b881e8eb04ef3b699fa7030e4670fab4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421470"
---
# <a name="sqlgetconnectoption-mapping"></a>Mapeamento SQLGetConnectOption
Quando um aplicativo chama **SQLGetConnectOption** por meio de um driver ODBC *3. x* , a chamada para  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 é mapeado da seguinte maneira:  
  
-   Se *fOption* indicar uma opção de conexão definida pelo ODBC que retorna uma cadeia de caracteres, o Gerenciador de driver chamará  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de conexão definida pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver chamará  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de instrução definida pelo driver, o Gerenciador de driver chamará  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o argumento *ConnectionHandle* é definido como o valor em *HDBC*, o argumento de *atributo* é definido como o valor em *fOption*e o argumento *ValuePtr* é definido com o mesmo valor de *pvParam*.  
  
 Para opções de conexão de cadeia de caracteres definidas pelo ODBC, o Gerenciador de driver define o argumento *BufferLength* na chamada para **SQLGetConnectAttr** com o comprimento máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão não cadeia de caracteres, *BufferLength* é definido como 0.  
  
 Para um driver ODBC *3. x* , o Gerenciador de driver não verifica mais para ver se a *opção* está entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START. O driver deve verificar a validade dos valores de opção.
