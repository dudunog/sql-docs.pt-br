---
title: Solucionando problemas comuns de desempenho com índices de hash com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ebf3f066dec03ba9e9f74dfdf551ccaababf032
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927967"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>Solucionando problemas comuns de desempenho com índices de hash com otimização de memória
  Este tópico abordará a solução de problemas e como contornar problemas comuns com índices de hash.  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>A busca requer um subconjunto de colunas de chave de índice de hash  
 **Problema:** Os índices de hash exigem valores para todas as colunas de chave de índice para computar o valor de hash e localizar as linhas correspondentes na tabela de hash. Em virtude disso, se uma consulta inclui predicados de igualdade para apenas um subconjunto das chaves do índice na cláusula WHERE, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode usar uma busca de índice para localizar as linhas que correspondem aos predicados na cláusula WHERE.  
  
 Em contraste, índices ordenados, como os índices não clusterizados baseados em disco e os índices não clusterizados com otimização de memória, dão suporte à busca de índice em um subconjunto das colunas de chave de índice, desde que elas sejam as colunas principais do índice.  
  
 **Sintoma:** Isso resulta em uma degradação do desempenho, pois [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisa executar verificações de tabela completas em vez de uma busca de índice, que normalmente é uma operação mais rápida.  
  
 **Como solucionar problemas:** Além da degradação do desempenho, a inspeção dos planos de consulta mostrará uma verificação em vez de uma busca de índice. Se a consulta for bem simples, a inspeção do texto da consulta e da definição de índice também mostrará se a busca requer um subconjunto das colunas de chave de índice.  
  
 Considere a seguinte tabela e consulta:  
  
```sql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 A tabela tem um índice de hash nas duas colunas (o_id, od_id), enquanto a consulta tem um predicado de igualdade (o_id). Como a consulta tem predicados de igualdade em apenas um subconjunto das colunas de chave de índice, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode executar uma operação de busca de índice usando PK_od; em vez disso, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisa reverter para uma verificação de índice completo.  
  
 **Soluções alternativas:** Há uma série de possíveis soluções alternativas. Por exemplo:  
  
-   Recrie o índice como o tipo não clusterizado em vez do hash não clusterizado. O índice não clusterizado com otimização de memória é ordenado e, portanto, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode executar uma busca de índice nas colunas principais de chave de índice. A definição de chave primária resultante para o exemplo seria `constraint PK_od primary key nonclustered`.  
  
-   Alterar a chave de índice atual para corresponder às colunas na cláusula WHERE.  
  
-   Adicionar um novo índice de hash que corresponde às colunas na cláusula WHERE da consulta. No exemplo, a definição da tabela resultante teria esta aparência:  
  
    ```sql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 Observe que um índice de hash com otimização de memória não apresenta o desempenho ideal quando há muitas linhas duplicadas para um valor de chave de índice específico: no exemplo, se o número de valores exclusivos para a coluna o_id fosse bem menor do que o número de linhas na tabela, o ideal não seria adicionar um índice (o_id); a melhor solução seria alterar o tipo de índice PK_od de hash para não clusterizado. Para obter mais informações, consulte [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Índices em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
