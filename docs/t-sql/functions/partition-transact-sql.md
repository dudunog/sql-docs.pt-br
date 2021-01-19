---
description: $PARTITION (Transact-SQL)
title: $PARTITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- $partition_TSQL
- $partition
dev_langs:
- TSQL
helpviewer_keywords:
- $PARTITION function
- partitions [SQL Server], numbers
ms.assetid: abc865d0-57a8-49da-8821-29457c808d2a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e32332d4b258a4fb37b49aa4d6715483998cd83d
ms.sourcegitcommit: 23649428528346930d7d5b8be7da3dcf1a2b3190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241858"
---
# <a name="partition-transact-sql"></a>$PARTITION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o número da partição na qual um conjunto de valores de coluna de particionamento são mapeados para qualquer função de partição especificada no [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
[ database_name. ] $PARTITION.partition_function_name(expression)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name*  
 É o nome do banco de dados que contém a função de partição.  
  
 *partition_function_name*  
 É o nome de qualquer função de partição existente na qual um conjunto de valores de coluna de particionamento é aplicado.  
  
 *expressão*  
 É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) cujo tipo de dados deve corresponder ou pode ser convertido implicitamente no tipo de dados de sua coluna de particionamento correspondente. *expression* também pode ser o nome de uma coluna de particionamento que participe atualmente de *partition_function_name*.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 $PARTITION retorna um valor **int** entre 1 e o número de partições da função de partição.  
  
 $PARTITION retorna o número de partição para qualquer valor válido, independentemente de o valor existir atualmente em um índice ou uma tabela particionada que use a função de partição.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-getting-the-partition-number-for-a-set-of-partitioning-column-values"></a>a. Obtendo o número de partições para um conjunto de valores de coluna de particionamento  
 O exemplo a seguir cria uma função de partição `RangePF1` que dividirá uma tabela ou índice em quatro partições. $PARTITION é usado para determinar se o valor `10`, representando a coluna de particionamento de `RangePF1`, será colocado na partição 1 da tabela.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PARTITION FUNCTION RangePF1 ( INT )  
AS RANGE FOR VALUES (10, 100, 1000) ;  
GO  
SELECT $PARTITION.RangePF1 (10) ;  
GO  
```  
  
### <a name="b-getting-the-number-of-rows-in-each-nonempty-partition-of-a-partitioned-table-or-index"></a>B. Obtendo o número de linhas em cada partição não vazia de um índice ou tabela particionada  
 O exemplo a seguir retorna o número de linhas em cada partição de tabela `TransactionHistory` que contém dados. A tabela `TransactionHistory` usa a função de partição `TransactionRangePF1` e é particionada na coluna `TransactionDate`.  
  
 Para executar esse exemplo, você deve primeiro executar o script PartitionAW.sql no banco de dados de amostra [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para obter mais informações, consulte [PartitioningScript](https://go.microsoft.com/fwlink/?LinkId=201015).  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT $PARTITION.TransactionRangePF1(TransactionDate) AS Partition,   
COUNT(*) AS [COUNT] FROM Production.TransactionHistory   
GROUP BY $PARTITION.TransactionRangePF1(TransactionDate)  
ORDER BY Partition ;  
GO  
```  
  
### <a name="c-returning-all-rows-from-one-partition-of-a-partitioned-table-or-index"></a>C. Retornando todas as linhas de uma partição de um índice ou tabela particionada  
 O exemplo a seguir retorna todas as linhas que estão na partição `5` da tabela `TransactionHistory`.  
  
> [!NOTE]  
>  Para executar esse exemplo, você deve primeiro executar o script PartitionAW.sql no banco de dados de amostra [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para obter mais informações, consulte [PartitioningScript](https://go.microsoft.com/fwlink/?LinkId=201015).  
  
```sql  
SELECT * FROM Production.TransactionHistory  
WHERE $PARTITION.TransactionRangePF1(TransactionDate) = 5 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
  
