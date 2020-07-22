---
title: GETDATE (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a função GETDATE, que retorna a hora do sistema do banco de dados atual como um valor de datetime.
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GETDATE_TSQL
- GETDATE
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- GETDATE function [SQL Server]
- current date and time [SQL Server]
- time [SQL Server], current
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- date and time [SQL Server], GETDATE
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: bebe3b65-2b3e-4c73-bf80-ff1132c680a7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4458702bc53bdec44bd5f690568bcbd06db6b12
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484577"
---
# <a name="getdate-transact-sql"></a>GETDATE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Retorna o carimbo de data/hora do sistema do banco de dados atual como um valor de **datetime** sem o deslocamento de fuso horário do banco de dados. Esse valor é derivado do sistema operacional do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.

> [!NOTE]
>  SYSDATETIME e SYSUTCDATETIME têm mais precisão de segundos fracionários que GETDATE e GETUTCDATE. SYSDATETIMEOFFSET inclui o deslocamento de fuso horário do sistema. SYSDATETIME, SYSUTCDATETIME e SYSDATETIMEOFFSET podem ser atribuídos a uma variável de qualquer um dos tipos de data e hora.

 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
GETDATE()
```

## <a name="return-type"></a>Tipo de retorno
 **datetime**

## <a name="remarks"></a>Comentários
 Instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] podem se referir a GETDATE sempre que puderem fazer referência a uma expressão **datatime**.

 GETDATE é uma função não determinística. Exibições e expressões que fazem referência a essa função em uma coluna não podem ser indexadas.

 Usar SWITCHOFFSET com a função GETDATE() pode fazer com que a consulta seja executada de forma mais lenta porque o otimizador de consulta não é capaz de obter estimativas de cardinalidade para o valor de GETDATE. É recomendável que você pré-calcule o valor de GETDATE e depois especifique esse valor na consulta, como mostrado no exemplo a seguir. Além disso, use a dica de consulta OPTION (RECOMPILE) para forçar o otimizador de consulta a recompilar um plano de consulta da próxima vez que a mesma consulta for executada. O otimizador terá, então, estimativas de cardinalidade precisas para GETDATE() e produzirá um plano de consulta mais eficiente.

```sql
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');
SELECT * FROM t
WHERE c1 > @dt OPTION (RECOMPILE);
```

## <a name="examples"></a>Exemplos
 Os exemplos a seguir usam as seis funções de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam a data e a hora atuais para retornar a data, a hora ou ambas. Os valores são retornados em série; portanto, seus segundos fracionários podem ser diferentes.

### <a name="a-getting-the-current-system-date-and-time"></a>a. Obtendo a data e a hora atuais do sistema

```sql
SELECT SYSDATETIME()
    ,SYSDATETIMEOFFSET()
    ,SYSUTCDATETIME()
    ,CURRENT_TIMESTAMP
    ,GETDATE()
    ,GETUTCDATE();
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]

 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```

### <a name="b-getting-the-current-system-date"></a>B. Obtendo a data atual do sistema

```sql
SELECT CONVERT (date, SYSDATETIME())
    ,CONVERT (date, SYSDATETIMEOFFSET())
    ,CONVERT (date, SYSUTCDATETIME())
    ,CONVERT (date, CURRENT_TIMESTAMP)
    ,CONVERT (date, GETDATE())
    ,CONVERT (date, GETUTCDATE());
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
SYSDATETIME()          2007-05-03
SYSDATETIMEOFFSET()    2007-05-03
SYSUTCDATETIME()       2007-05-04
CURRENT_TIMESTAMP      2007-05-03
GETDATE()              2007-05-03
GETUTCDATE()           2007-05-04
```

### <a name="c-getting-the-current-system-time"></a>C. Obtendo a hora atual do sistema

```sql
SELECT CONVERT (time, SYSDATETIME())
    ,CONVERT (time, SYSDATETIMEOFFSET())
    ,CONVERT (time, SYSUTCDATETIME())
    ,CONVERT (time, CURRENT_TIMESTAMP)
    ,CONVERT (time, GETDATE())
    ,CONVERT (time, GETUTCDATE());
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
SYSDATETIME()       13:18:45.3490361
SYSDATETIMEOFFSET() 13:18:45.3490361
SYSUTCDATETIME()    20:18:45.3490361
CURRENT_TIMESTAMP   13:18:45.3470000
GETDATE()           13:18:45.3470000
GETUTCDATE()        20:18:45.3470000
```

## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 Os exemplos a seguir usam as três funções do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam a data e a hora atuais para retornar a data, a hora ou ambas. Os valores são retornados em série; portanto, seus segundos fracionários podem ser diferentes.

### <a name="d-getting-the-current-system-date-and-time"></a>D. Obtendo a data e a hora atuais do sistema

```sql
SELECT SYSDATETIME()
    ,CURRENT_TIMESTAMP
    ,GETDATE();
```

### <a name="e-getting-the-current-system-date"></a>E. Obtendo a data atual do sistema

```sql
SELECT CONVERT (date, SYSDATETIME())
    ,CONVERT (date, CURRENT_TIMESTAMP)
    ,CONVERT (date, GETDATE());
```

### <a name="f-getting-the-current-system-time"></a>F. Obtendo a hora atual do sistema

```sql
SELECT CONVERT (time, SYSDATETIME())
    ,CONVERT (time, CURRENT_TIMESTAMP)
    ,CONVERT (time, GETDATE());
```

## <a name="see-also"></a>Consulte Também
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
