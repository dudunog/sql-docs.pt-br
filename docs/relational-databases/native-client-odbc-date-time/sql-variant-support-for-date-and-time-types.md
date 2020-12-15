---
description: Suporte a Sql_variant para tipos de data e hora
title: Suporte a sql_variant para tipos de data e hora | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0d7570b35f3d65c9f092b346e81fc37556dc5f1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438509"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>Suporte a Sql_variant para tipos de data e hora
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Este tópico descreve como o tipo de dados **sql_variant** dá suporte à funcionalidade avançada de data e hora.  
  
 O atributo de coluna SQL_CA_SS_VARIANT_TYPE é usado para retornar o tipo C de uma coluna de resultado variável. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]O  apresenta um atributo adicional, SQL_CA_SS_VARIANT_SQL_TYPE, que define o tipo SQL de uma coluna de resultado variável no IRD (descritor de linha de implementação). SQL_CA_SS_VARIANT_SQL_TYPE também pode ser usado no IPD (descritor de parâmetro de implementação) para especificar o tipo SQL de um parâmetro SQL_SS_TIME2 ou SQL_SS_TIMESTAMPOFFSET com tipo SQL_C_BINARY C associado ao tipo SQL_SS_VARIANT.  
  
 Os novos tipos SQL_SS_TIME2 e SQL_SS_TIMESTAMPOFFSET podem ser definidos por SQLColAttribute. SQL_CA_SS_VARIANT_SQL_TYPE pode ser retornado por SQLGetDescField.  
  
 Em colunas de resultado, o driver será convertido da variante em tipos de data/hora. Para obter mais informações, consulte [conversões de SQL para C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Ao associar a SQL_C_BINARY, o comprimento do buffer deve ser grande o suficiente para receber a struct que corresponde ao tipo SQL.  
  
 Para os parâmetros SQL_SS_TIME2 e SQL_SS_TIMESTAMPOFFSET, o driver converterá valores de C em valores de **sql_variant** , conforme descrito na tabela a seguir. Se um parâmetro for associado como SQL_C_BINARY e o tipo de servidor for SQL_SS_VARIANT, ele será tratado como um valor binário, a menos que o aplicativo tenha definido SQL_CA_SS_VARIANT_SQL_TYPE como outro tipo SQL. Nesse caso, SQL_CA_SS_VARIANT_SQL_TYPE tem precedência; ou seja, caso SQL_CA_SS_VARIANT_SQL_TYPE seja definido, ele substitui o comportamento padrão de dedução do tipo SQL variável do tipo C.  
  
|Tipo de C|Tipo de servidor|Comentários|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_TINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_STINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_SHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_SSHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_USHORT|INT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_LONG|INT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_SLONG|INT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_ULONG|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_SBIGINT|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_DOUBLE|FLOAT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_UTINYINT|TINYINT|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE não é definido.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Scale é definido como SQL_DESC_PRECISION (o parâmetro *DecimalDigits* de **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Scale é definido como SQL_DESC_PRECISION (o parâmetro *DecimalDigits* de **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Scale é definido como SQL_DESC_PRECISION (o parâmetro *DecimalDigits* de **SQLBindParameter**).|  
|SQL_C_NUMERIC|decimal|A precisão é definida como SQL_DESC_PRECISION (o parâmetro *colunasize* de **SQLBindParameter**).<br /><br /> Conjunto de dimensionamento para SQL_DESC_SCALE (o parâmetro *DecimalDigits* de SQLBindParameter).|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE é ignorado|  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
