---
description: Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON (SQL Server)
title: Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff06a77af1592bf9bf2386742a53033ade76aecd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478117"
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

  A cláusula **FOR JSON** usa as regras a seguir para converter os tipos de dados do SQL Server em tipos JSON na saída JSON.  
  
|Categoria|Tipo de dados do SQL Server|Tipo de dados JSON|  
|--------------|--------------|---------------|  
|Tipos de cadeia de caracteres e caracteres|char, nchar, varchar, nvarchar|string|  
|Tipos numéricos|int, bigint, float, decimal, numeric|número|  
|Tipo de Bit|bit|Booliano (verdadeiro ou falso)|  
|Tipos de data e hora|date, datetime, datetime2, time, datetimeoffset|string|  
|Tipos binários|varbinary, binary, image, timestamp, rowversion|Cadeia de caracteres codificada em BASE64|  
|Tipos CLR|geometria, geografia, outros tipos CLR|Não há suporte. Estes tipos retornam um erro.<br /><br /> Na instrução SELECT, use CAST ou CONVERT ou use um método ou propriedade CLR para converter os dados de origem em um tipo de dados do SQL Server que pode ser convertido com êxito em um tipo JSON. Por exemplo, use **STAsText()** para o tipo de geometria ou **ToString()** para qualquer tipo CLR. O tipo do valor de saída JSON é derivado do tipo de retorno da conversão aplicada na instrução SELECT.|  
|Outros tipos|uniqueidentifier, money|string|  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
