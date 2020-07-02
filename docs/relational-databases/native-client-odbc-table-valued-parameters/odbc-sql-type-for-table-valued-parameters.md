---
title: Tipo ODBC SQL para parâmetros com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96e74ebafcf6d80ba3db5a609209dcb79339d71e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783189"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>Tipo ODBC SQL para parâmetros com valor de tabela
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  O suporte para parâmetros com valor de tabela é fornecido por um novo tipo ODBC SQL, SQL_SS_TABLE.  
  
## <a name="remarks"></a>Comentários  
 SQL_SS_TABLE não pode ser convertido em qualquer outro tipo de dados ODBC ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se SQL_SS_TABLE for usado como um tipo de dados C no parâmetro *ValueType* de SQLBindParameter, ou se for feita uma tentativa de definir SQL_DESC_TYPE em um registro APD (descritor de parâmetro de aplicativo) como SQL_SS_TABLE, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE = HY003, "tipo de buffer de aplicativo inválido".  
  
 Se SQL_DESC_TYPE for definido como SQL_SS_TABLE em um registro do IPD e o registro do descritor de parâmetro de aplicativo correspondente não for SQL_C_DEFAULT, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY003, "Tipo de buffer de aplicativo inválido". Isso pode ocorrer com o *ParameterType* de SQLSetDescField, SQLSetDescRec ou SQLBindParameter.  
  
 Se o parâmetro *TargetType* for SQL_SS_TABLE ao chamar SQLGetData, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE = HY003, "tipo de buffer de aplicativo inválido".  
  
 Não é possível associar uma coluna de parâmetros com valor de tabela como o tipo SQL_SS_TABLE. Se **SQLBindParameter** for chamado com *ParameterType* definido como SQL_SS_TABLE, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY004, "Tipo de dados SQL inválido". Isso também pode ocorrer com SQLSetDescField e SQLSetDescRec.  
  
 Os valores de coluna de parâmetros com valor de tabela têm as mesmas opções de conversão de dados que as colunas de parâmetros e resultados.  
  
 Um parâmetro com valor de tabela pode ser um parâmetro de entrada somente no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior. Se for feita uma tentativa de definir SQL_DESC_PARAMETER_TYPE com um valor diferente de SQL_PARAM_INPUT por meio de SQLBindParameter ou SQLSetDescField, SQL_ERROR será retornado e um registro de diagnóstico será adicionado à instrução com SQLSTATE = HY105 e a mensagem "tipo de parâmetro inválido".  
  
 As colunas de parâmetros com valor de tabela não podem usar SQL_DEFAULT_PARAM em *StrLen_or_IndPtr*, porque não há suporte para valores padrão por linha com parâmetros com valor de tabela. Em vez disso, um aplicativo pode definir o atributo de coluna SQL_CA_SS_COL_HAS_DEFAULT_VALUE como 1. Isso significa que a coluna terá valores padrão para todas as linhas. Se *StrLen_or_IndPtr* for definido como SQL_DEFAULT_PARAM, SQLExecute ou SQLExecDirect retornará SQL_ERROR e um registro de diagnóstico será adicionado à instrução com SQLSTATE = HY090 e a mensagem "comprimento de buffer ou de cadeia de caracteres inválido".  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
