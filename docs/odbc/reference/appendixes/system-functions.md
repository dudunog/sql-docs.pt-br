---
title: Funções do sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302827"
---
# <a name="system-functions"></a>Funções de sistema
A tabela a seguir lista as funções de sistema incluídas no conjunto de funções escalares ODBC. Ao chamar **SQLGetInfo** com um *tipo de informação* de SQL_SYSTEM_FUNCTIONS, um aplicativo pode determinar quais funções do sistema têm suporte de um driver.  
  
 Os argumentos indicados como *exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um literal, em que o tipo de dados subjacente poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 Os argumentos denotados como *valor* podem ser uma constante literal, em que o tipo de dados subjacente pode ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 Os valores retornados são representados como tipos de dados ODBC.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**Banco de dados ()** (ODBC 1,0)|Retorna o nome do banco de dados correspondente ao identificador de conexão. (O nome do banco de dados também está disponível chamando **SQLGetConnectOption** com a opção de conexão SQL_CURRENT_QUALIFIER.)|  
|**IFNULL (** _exp_,_valor_**)** (ODBC 1,0)|Se *exp* for nulo, o *valor* será retornado. Se *exp* não for NULL, *exp* será retornado. O tipo de dados possível ou tipos de *valor* devem ser compatíveis com o tipo de dados *exp*.|  
|**User ()** (ODBC 1,0)|Retorna o nome de usuário no DBMS. (O nome de usuário também está disponível por meio de **SQLGetInfo** especificando o tipo de informação: SQL_USER_NAME.) Isso pode ser diferente do nome de logon.|
