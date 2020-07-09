---
title: YEAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b48d0a768bae5a058c2868ae3b30f3f48f06ef40
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85991430"
---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna um inteiro que representa o ano da *data* especificada.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. O argumento *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou um literal de cadeia de caracteres.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
 YEAR retorna o mesmo valor que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**year**, *date*).  
  
 Se *date* contiver apenas uma parte de hora, o valor retornado será 1900, o ano base.  
  
## <a name="examples"></a>Exemplos  
 A instrução a seguir retorna `2010`. Este é o número do ano.  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 A instrução a seguir retorna `1900, 1, 1`. O argumento para *date* é o número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A instrução a seguir retorna `1900, 1, 1`. O argumento para *date* é o número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

