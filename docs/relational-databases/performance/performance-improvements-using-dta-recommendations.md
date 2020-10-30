---
title: Melhorias de desempenho recomendadas do DTA
description: Saiba como o Orientador de Otimização do Mecanismo de Banco de Dados pode recomendar uma combinação de índices rowstore e columnstore analisando uma carga de trabalho de banco de dados no SQL Server.
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8c64f567d8da74a2eb15b5647a2b259ba52193b4
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678951"
---
# <a name="performance-improvements-using-database-engine-tuning-advisor-dta-recommendations"></a>Melhorias de desempenho usando as recomendações do DTA (Orientador de Otimização do Mecanismo de Banco de Dados)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]


---
O desempenho de cargas de trabalho analíticas e do data warehouse pode se beneficiar muito com índices **columnstore** , especialmente em consultas que precisam examinar tabelas grandes. Os índices **rowstore** (B+-árvore) são mais eficientes para consultas que acessam quantidades de dados relativamente pequenas, em uma pesquisa de determinado valor ou intervalo de valores. Como os índices rowstore podem fornecer linhas em ordem classificada, eles também podem reduzir o custo de classificação em planos de execução de consulta. Portanto, a escolha de qual combinação de índices columnstore e rowstore deve ser criada depende da carga de trabalho do aplicativo.

A partir do SQL Server 2016, o DTA (Orientador de Otimização do Mecanismo de Banco de Dados) pode recomendar uma **combinação adequada de índices rowstore e columnstore** analisando uma carga de trabalho de banco de dados específica. 

Para demonstrar os benefícios das recomendações do DTA no desempenho da carga de trabalho, tentei isso com várias cargas de trabalho reais do cliente. Para cada carga de trabalho do cliente, deixamos o DTA analisar consultas individuais, bem como a carga de trabalho total das consultas. Consideramos três alternativas:
  
  1. **Somente columnstore** : crie apenas índices columnstore para todas as tabelas sem usar o DTA. 
  2. **DTA (somente rowstore)** : execute o DTA com a opção para recomendar índices somente rowstore.
  3. **DTA (rowstore + columnstore)** : Execute o DTA com a opção de recomendar índices columnstore e rowstore.  
   
Em cada caso, depois implementamos os índices recomendados. Relatamos o Tempo de CPU (em milissegundos) com a média calculada em várias execuções da consulta ou da carga de trabalho. A figura abaixo plota o tempo de CPU em milissegundos para cargas de trabalho entre dois bancos de dados de cliente diferentes. Observe que o eixo Y (Tempo de CPU) usa uma escala logarítmica.   


![Captura de tela de um gráfico de barras mostrando o desempenho de columnstore e rowstore do DTA.](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**Necessário para designs físicos mistos** : o primeiro conjunto de barras correspondente ao Cliente 1 Consulta 1. O DTA (rowstore + columnstore) recomenda um conjunto de quatro índices columnstore e seis índices rowstore que resulta em um tempo de CPU 2,5X – 4X menor comparado ao somente índice columnstore e DTA (somente rowstore). Isso demonstra os benefícios de designs físicos mistos formados por índices columnstore e rowstore *mesmo para uma única consulta* . 

**Eficiência das recomendações de índice rowstore** : o segundo e o terceiro conjuntos de barras (correspondentes ao Cliente 1 Consulta 2 e ao Cliente 2 Consulta 1) são casos em que as consultas têm predicados de filtro seletivos que se beneficiam de índices rowstore adequados. Para essas duas consultas, o DTA (somente rowstore) e DTA (rowstore + columnstore) recomenda somente índices rowstore. Esses exemplos também mostram que, mesmo quando o DTA é invocado com a opção para recomendar índices columnstore, sua abordagem baseada em custos garante que ele recomendará um índice columnstore somente se a carga de trabalho realmente puder se beneficiar com ele.

**Eficiência das recomendações de índice columnstore** : o quarto conjunto de barras correspondente ao Cliente 2 Consulta 2 representa um caso em que a consulta examina tabelas grandes que se beneficiariam de índices columnstore. O DTA (somente rowstore) gera uma recomendação cujo Tempo de CPU é mais alto comparado com quando os índices columnstore estão presentes. O DTA (rowstore + columnstore) recomenda índices columnstore adequados, encontrando a correspondência do desempenho de execução da consulta da opção somente columnstore.

**Eficiência das recomendações de carga de trabalho com várias consultas** : o conjunto final de barras correspondente à carga de trabalho completa do Cliente 2 exemplifica a capacidade do DTA de analisar várias consultas na carga de trabalho para recomendar um conjunto adequado de índices rowstore e columnstore que pode melhorar o custo geral de execução da carga de trabalho. O DTA (rowstore + columnstore) recomenda quatro índices columnstore e dezenas de índices rowstore que resultam em uma melhoria que supera uma ordem de magnitude para a carga de trabalho quando comparado à opção que cria somente índices columnstore e em uma melhoria de cerca de 4X a 5X quando comparado ao DTA (somente rowstore).

Em resumo, os exemplos acima ilustram a capacidade do DTA de utilizar de forma conveniente índices rowstore e columnstore com suporte no Mecanismo de Banco de Dados do SQL Server, além de recomendar uma combinação apropriada de índices que pode reduzir consideravelmente o Tempo de CPU da carga de trabalho. 

<a name="see-also"></a>Consulte Também
---
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Recomendações de índice columnstore no DTA (Orientador de Otimização do Mecanismo de Banco de Dados)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Guia de Índices columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)

[Índices columnstore para Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



