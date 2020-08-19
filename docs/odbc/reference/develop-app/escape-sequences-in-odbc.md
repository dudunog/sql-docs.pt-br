---
description: Sequências de escape no ODBC
title: Sequências de escape no ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62745b749870fa33151fc1a5f6bd3a1bfc344ad7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429308"
---
# <a name="escape-sequences-in-odbc"></a>Sequências de escape no ODBC
Vários recursos de linguagem, como junções externas e chamadas de função escalar, são normalmente implementados por DBMSs. No entanto, as sintaxes para esses recursos tendem a ser específicas do DBMS, mesmo quando as sintaxes padrão são definidas por vários órgãos de padrões. Por isso, o ODBC define as sequências de escape que contêm as sintaxes padrão para os seguintes recursos de idioma:  
  
-   Literais data, time, timestamp e DateTime Interval  
  
-   Funções escalares, como funções numéricas, de cadeia de caracteres e de conversão de tipo de dados  
  
-   Caractere de escape de predicado LIKE  
  
-   Junções externas  
  
-   Chamadas de procedimento  
  
 A sequência de escape usada pelo ODBC é a seguinte:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Comentários  
 A sequência de escape é reconhecida e analisada por drivers, que substituem as seqüências de escape por gramática específica do DBMS. Para obter mais informações sobre a sintaxe de sequência de escape, consulte [sequências de escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) no Apêndice C: gramática SQL.  
  
> [!NOTE]  
>  No ODBC 2. *x*, essa foi a sintaxe padrão da sequência de escape: **--( \* fornecedor (**_nome do fornecedor_**), extensão do produto (nome do**_produto_**)**_extension_ ** \* )--**  
>   
>  Além dessa sintaxe, uma sintaxe abreviada foi definida no formato:            **{**_Extension_**}**  
>   
>  No ODBC 3. *x*, a forma longa da sequência de escape foi preterida e a forma abreviada é usada exclusivamente.  
  
 Como as sequências de escape são mapeadas pelo driver para sintaxes específicas do DBMS, um aplicativo pode usar a sequência de escape ou a sintaxe específica do DBMS. No entanto, os aplicativos que usam a sintaxe específica do DBMS não serão interoperáveis. Ao usar a sequência de escape, os aplicativos devem verificar se o atributo da instrução SQL_ATTR_NOSCAN está desativado, o que é por padrão. Caso contrário, a sequência de escape será enviada diretamente para a fonte de dados, onde geralmente causará um erro de sintaxe.  
  
 Os drivers dão suporte apenas às sequências de escape que eles podem mapear para os recursos de linguagem subjacente. Por exemplo, se a fonte de dados não oferecer suporte a junções externas, nenhum será o driver. Para determinar quais sequências de escape têm suporte, um aplicativo chama **SQLGetTypeInfo** e **SQLGetInfo**. Para obter mais informações, consulte a próxima seção, [data, hora e literais de carimbo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de hora.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Data, hora e literais de carimbo de data/hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chamadas de função escalar](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Caractere de escape de predicado LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Junções externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md)
