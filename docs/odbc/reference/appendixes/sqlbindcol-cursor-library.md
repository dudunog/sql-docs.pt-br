---
description: SQLBindCol (Biblioteca de cursores)
title: SQLBindCol (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3b3968687f1c9062457a16ec7c5bc11cb32d3a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456475"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindCol** na biblioteca de cursores. Para obter informações gerais sobre **SQLBindCol**, consulte [SQLBindCol function](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Um aplicativo aloca um ou mais buffers para a biblioteca de cursores retornar o conjunto de linhas atual. Ele chama **SQLBindCol** uma ou mais vezes para associar esses buffers ao conjunto de resultados.  
  
 Um aplicativo pode chamar **SQLBindCol** para reassociar colunas de conjunto de resultados depois de chamar **SQLExtendedFetch**, **SQLFetch**ou **SQLFetchScroll**, desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna associada permaneçam os mesmos. O aplicativo não precisa fechar o cursor para reassociar colunas a endereços diferentes.  
  
 A biblioteca de cursores dá suporte à definição do atributo instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de ligação. (**SQLBindCol** não precisa ser chamado para que essa reassociação ocorra.) Se a biblioteca de cursores for usada com um driver ODBC *3. x* , o deslocamento de ligação não será usado quando **SQLFetch** for chamado. O deslocamento de ligação será usado se **SQLFetch** for chamado quando a biblioteca de cursores for usada com um driver ODBC *2. x* porque **SQLFetch** é então mapeado para **SQLExtendedFetch**.  
  
 A biblioteca de cursores dá suporte à chamada de **SQLBindCol** para associar a coluna de indicador.  
  
 Ao trabalhar com um driver ODBC *2. x* , a biblioteca de cursores retorna SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) quando **SQLBindCol** é chamado para definir o comprimento do buffer para uma coluna de indicador como um valor diferente de 4. Ao trabalhar com um driver ODBC *3. x* , a biblioteca de cursores permite que o buffer seja de qualquer tamanho.
