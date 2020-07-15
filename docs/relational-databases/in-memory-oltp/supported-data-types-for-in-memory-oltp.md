---
title: Tipos de dados com suporte para o OLTP in-memory | Microsoft Docs
description: Saiba mais sobre os tipos de dados que não são compatíveis com as tabelas com otimização de memória, os recursos de OLTP in-memory e os módulos T-SQL compilados nativamente.
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 324d9c27608bd5ee3e93a6987cec7b81407f048a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650924"
---
# <a name="supported-data-types-for-in-memory-oltp"></a>Tipos de Dados com Suporte para o OLTP na Memória
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este artigo lista os tipos de dados que não têm suporte para os recursos do OLTP na Memória:  
  
-   Tabelas com otimização de memória  
  
-   Módulos do T-SQL compilados nativamente  
  
## <a name="unsupported-data-types"></a>Tipos de dados sem-suporte  
 Não há suporte para os seguintes tipos de dados:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Tipos definidos pelo usuário|.|  
  
## <a name="notable-supported-data-types"></a>Tipos de Dados com Suporte Importantes  
 A maioria dos tipos de dados é suportada pelos recursos do OLTP na Memória. Vale a pena observar explicitamente o seguinte:  
  
|Tipos de cadeia de caracteres e binários|Para obter mais informações|  
|-----------------------------|--------------------------|  
|binary e varbinary*|[binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char e varchar*|[char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar e nvarchar*|[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
Para os tipos de dados da cadeia de caracteres e binários anteriores, começando com o SQL Server 2016:  
  
- Uma tabela individual com otimização de memória também pode ter várias colunas longas, como `nvarchar(4000)`, mesmo que seus tamanhos somem mais do que o tamanho físico da linha com 8.060 bytes.  
  
- Uma tabela com otimização de memória pode ter colunas da cadeia de caracteres e binárias com um tamanho máximo dos tipos de dados, como `varchar(max)`.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>Identificar LOBs e outras colunas que estão fora de linha

Começando com o SQL Server 2016, as tabelas com otimização de memória [dão suporte a colunas fora de linha](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md), permitindo que uma única linha da tabela seja maior que 8060 bytes. A instrução SELECT do Transact-SQL a seguir relata todas as colunas que estão fora de linha em tabelas com otimização de memória. Observe que:

- Todas as colunas de chave de índice são armazenadas em linha.
  - Chaves de índice não exclusivas agora podem incluir colunas que permitem valor nulo, em tabelas com otimização de memória.
  - Índices podem ser declarados como UNIQUE em uma tabela com otimização de memória.
- Todas as colunas LOB são armazenadas fora de linha.
- Um max_length de -1 indica uma coluna LOB (objeto grande).


```sql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


### <a name="other-data-types"></a>Outros tipos de dados


|Outros Tipos|Para obter mais informações|  
|-----------------|--------------------------|  
|tipos de tabela|[Variáveis de tabela com otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao Transact-SQL para OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementando SQL_VARIANT em uma tabela com otimização de memória](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
 [Tamanho da tabela e de linha em tabelas com otimização de memória](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
