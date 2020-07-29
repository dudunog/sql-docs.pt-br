---
title: Monitorar T-SQL com eventos estendidos
description: Saiba como usar eventos estendidos para monitorar e solucionar problemas de instruções T-SQL PREDICT nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/24/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d3be71d304cb17392fcc4ec5a8796588de9d884
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352313"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>Monitorar instruções T-SQL PREDICT com eventos estendidos nos Serviços de Machine Learning do SQL Server

Saiba como usar eventos estendidos para monitorar e solucionar problemas de instruções T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) nos Serviços de Machine Learning do SQL Server.

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

Os seguintes eventos estendidos estão disponíveis em todas as versões do SQL Server compatíveis com a instrução T-SQL [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql). 

|name |object_type|descrição| 
|----|----|----|
|predict_function_completed |event  |Detalhamento do tempo de execução interno|
|predict_model_cache_hit |event|Ocorre quando um modelo é recuperado do cache de modelo da função PREDICT. Use esse evento junto com outros predict_model_cache_* para solucionar problemas causados pelo cache de modelo da função PREDICT.|
|predict_model_cache_insert |event  |   Ocorre quando um modelo é inserido no cache de modelo da função PREDICT. Use esse evento junto com outros predict_model_cache_* para solucionar problemas causados pelo cache de modelo da função PREDICT.    |
|predict_model_cache_miss   |event|Ocorre quando um modelo não é encontrado no cache de modelo da função PREDICT. Ocorrências frequentes desse evento podem indicar que o SQL Server precisa de mais memória. Use esse evento junto com outros predict_model_cache_* para solucionar problemas causados pelo cache de modelo da função PREDICT.|
|predict_model_cache_remove |event| Ocorre quando um modelo é removido do cache de modelo da função PREDICT. Use esse evento junto com outros predict_model_cache_* para solucionar problemas causados pelo cache de modelo da função PREDICT.|

## <a name="query-for-related-events"></a>Consultar eventos relacionados

Para exibir uma lista de todas as colunas retornadas para esses eventos, execute a seguinte consulta no SQL Server Management Studio:

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Exemplos

Para capturar informações sobre o desempenho de uma sessão de pontuação usando PREDICT:

1. Crie uma nova sessão de evento estendido usando o Management Studio ou outra [ferramenta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools) compatível.
2. Adicione os eventos `predict_function_completed` e `predict_model_cache_hit` à sessão.
3. Inicie a sessão de evento estendido.
4. Execute a consulta que usa PREDICT.

Nos resultados, examine estas colunas:

+ O valor de `predict_function_completed` mostra quanto tempo a consulta gastou ao carregar o modelo e a pontuação.
+ O valor booliano de `predict_model_cache_hit` indica se a consulta usou um modelo em cache ou não. 

### <a name="native-scoring-model-cache"></a>Cache de modelo de pontuação nativa

Além dos eventos específicos de PREDICT, você pode usar as consultas a seguir para saber mais sobre o uso do cache e do modelo em cache:

Exibir o cache de modelo de pontuação nativa:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Exibir os objetos no cache de modelo:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre eventos estendidos (às vezes chamados de XEvents) e como rastrear eventos em uma sessão, confira estes artigos:

+ [Monitorar scripts do Python e do R com eventos estendidos nos Serviços de Machine Learning do SQL Server](extended-events.md)
+ [Arquitetura e conceitos de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar a captura de eventos no SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gerenciar sessões de evento no Pesquisador de Objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
