---
title: Tipos de dados padrão do C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307047"
---
# <a name="default-c-data-types"></a>Tipos de dados do C padrão
Se um aplicativo especificar SQL_C_DEFAULT em **SQLBindCol**, **SQLGetData**ou **SQLBindParameter**, o driver assumirá que o tipo de dados C do buffer de saída ou de entrada corresponde ao tipo de dados SQL da coluna ou parâmetro ao qual o buffer está associado.  
  
> [!IMPORTANT]  
>  Aplicativos interoperáveis não devem usar SQL_C_DEFAULT. Em vez disso, eles sempre devem especificar o tipo C do buffer que estão usando. Isso ocorre porque os drivers nem sempre determinam corretamente o tipo C padrão, pelos seguintes motivos:  
  
-   Se o DBMS promover um tipo de dados SQL de uma coluna ou parâmetro, o driver não poderá determinar o tipo de dados SQL original de uma coluna ou parâmetro. Portanto, ele não pode determinar o tipo de dados padrão do C correspondente.  
  
-   Se o driver não puder determinar se uma determinada coluna ou parâmetro é assinado, como geralmente é o caso quando isso é manipulado pelo DBMS, o driver não pode determinar se o tipo de dados C padrão correspondente deve ser assinado ou não assinado.  
  
     Como SQL_C_DEFAULT é fornecido apenas como uma conveniência de programação, o aplicativo não perde nenhuma funcionalidade quando especifica o tipo de dados C real.  
  
 Uma tabela que mostra o tipo de dados C padrão para cada tipo de dados SQL é incluída na [conversão de dados de tipos de dados SQL para C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), posteriormente neste apêndice.
