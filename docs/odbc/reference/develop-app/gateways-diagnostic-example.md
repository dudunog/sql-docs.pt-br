---
description: Exemplo de diagnóstico de gateways
title: Exemplo de diagnóstico de gateways | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17e32f0ccdc1b2fbbebb1969083e216ed3371688
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465778"
---
# <a name="gateways-diagnostic-example"></a>Exemplo de diagnóstico de gateways
Em uma arquitetura de gateway, um driver envia solicitações para um gateway que oferece suporte a ODBC. O gateway envia as solicitações para um DBMS. Por ser o componente que faz interface com o Gerenciador de driver, o driver formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se a Oracle tiver baseado em um gateway para RDB no Microsoft Open Data Services e se o RDB não puder encontrar o funcionário da tabela, o gateway poderá gerar essa mensagem de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Como o erro ocorreu na fonte de dados, o gateway adicionou um prefixo para o identificador de fonte de dados ([RDB]) à mensagem de diagnóstico. Como o gateway era o componente que interfrenteu com a fonte de dados, ele adicionou prefixos para seu fornecedor ([DEC]) e identificador ([gateway de ODS]) à mensagem de diagnóstico. Ele também adicionou o valor SQLSTATE e o código de erro RDB ao início da mensagem de diagnóstico. Isso permitia que ele preservasse a semântica de sua própria estrutura de mensagens e ainda forneceria as informações de diagnóstico do ODBC para o driver. O driver analisa as informações de erro anexadas à instrução de erro pelo Gateway.  
  
 Como o driver de gateway é o componente que faz interface com o Gerenciador de driver, ele usaria a mensagem de diagnóstico anterior para formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
