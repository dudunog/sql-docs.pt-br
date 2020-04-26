---
title: Conversão de dados de parâmetro com valor de tabela e outros erros e avisos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 576e8e49411412264afc5828fe606a19cc3751f6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62468249"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversão de dados de parâmetros com valor de tabela e outros erros e avisos
  Valores da coluna de parâmetros com valor de tabela podem ser convertidos entre tipos de dados de cliente e servidor da mesma forma que outros valores de parâmetro e coluna. Mas como um parâmetro com valor de tabela pode conter várias colunas e várias linhas, é importante conseguir identificar o valor real quando o erro ocorrer.  
  
 Quando um erro ou aviso é detectado em uma coluna de parâmetro com valor de tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gerará um registro diagnóstico. A mensagem de erro conterá o número de parâmetro com valor de tabela, assim como o número da linha e o ordinal da coluna. Um aplicativo também pode usar os campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER dentro dos registros de diagnóstico para determinar quais valores são associados a erros e avisos. Estes campos de diagnóstico estão disponíveis no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores.  
  
 Os componentes de mensagem e SQLSTATE dos registros de diagnóstico estarão em conformidade com o comportamento de ODBC existente em todos os níveis. Ou seja, exceto para as informações de identificação de parâmetro, linha e coluna, as mensagens de erro têm os mesmos valores para parâmetros com valor de tabela como seriam para parâmetros com valor não tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
