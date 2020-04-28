---
title: 'C to SQL: bit | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a96982573d83cf01947f82dc2014ee2c470931e3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292039"
---
# <a name="c-to-sql-bit"></a>C para SQL: bit
O identificador para o tipo de dados ODBC C é:  
  
 SQL_C_BIT  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados de bits C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Nenhum|n/d|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL SQL_FLOAT<br /><br /> SQL_DOUBLE|Nenhum|n/d|  
|SQL_BIT|Nenhum|n/d|  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados bit C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados bit C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
