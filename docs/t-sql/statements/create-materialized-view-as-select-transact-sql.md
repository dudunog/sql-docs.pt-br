---
title: CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 73fcf068c55b28448d87245b380281b461ef36b0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633604"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Este artigo explica a instrução criar CREATE MATERIALIZED VIEW AS SELECT T-SQL no SQL Data Warehouse do Azure para o desenvolvimento de soluções. O artigo também fornece exemplos de códigos.

Uma Exibição Materializada persiste os dados retornados da consulta de definição de exibição e é atualizada automaticamente conforme os dados são alterados nas tabelas subjacentes.   Ela melhora o desempenho de consultas complexas (normalmente consultas com junções e agregações) e oferece operações simples de manutenção.   Com seu recurso de correspondência automática do plano de execução, uma exibição materializada não precisa ser referenciada na consulta para o otimizador considerar a exibição na substituição.  Essa capacidade permite que os engenheiros de dados implementem as exibições materializadas como um mecanismo para melhorar o tempo de resposta de consulta sem precisar alterar as consultas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```  
  
## <a name="arguments"></a>Argumentos

*schema_name*     
 É o nome do esquema ao qual a exibição pertence.  
  
*materialized_view_name*   
É o nome da exibição. Os nomes de exibição devem seguir as regras para identificadores. A especificação do nome do proprietário da exibição é opcional.  

*opções de distribuição*     
Somente distribuições de HASH e ROUND_ROBIN são compatíveis.

*select_statement*   
A lista SELECT na definição de exibição materializada precisa cumprir ao menos um desses dois critérios:
- A lista SELECT contém uma função de agregação.
- GROUP BY é usada na definição da Exibição materializada e todas as colunas em GROUP BY são incluídas na lista SELECT.  Até 32 colunas podem ser usadas na cláusula GROUP BY.

As funções de agregação são necessárias na lista SELECT da definição da exibição materializada.  As agregações com suporte incluem MAX, MIN, AVG, COUNT, COUNT_BIG, SUM, VAR, STDEV.

Quando as agregações MIN/MAX são usadas na lista SELECT da definição da exibição materializada, os seguintes requisitos se aplicam:
 
- FOR_APPEND é necessária.  Por exemplo:
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- A exibição materializada será desabilitada quando UPDATE ou DELETE ocorrerem nas tabelas base referenciadas.  Essa restrição não se aplica a INSERTs.  Para habilitar novamente a exibição materializada, execute ALTER MATERIALIZED VIEW com REBUILD.
  
## <a name="remarks"></a>Comentários

Uma exibição materializada no data warehouse do Azure é semelhante a uma exibição indexada no SQL Server.  Ela compartilha quase as mesmas restrições que a exibição indexada (confira [Criar exibições indexadas](/sql/relational-databases/views/create-indexed-views) para obter detalhes), exceto pelo fato de que uma exibição materializada dá suporte a funções de agregação.   

Somente o CLUSTERED COLUMNSTORE INDEX é compatível com a exibição materializada. 

Uma exibição materializada não pode referenciar outras exibições.  

Uma exibição materializada não pode ser criada em uma tabela DDM (máscara de dados dinâmicos), mesmo que a coluna DDM não faça parte da exibição materializada.  Se uma coluna de tabela fizer parte de uma exibição materializada ativa ou de uma exibição materializada desabilitada, o DDM não poderá ser adicionado a essa coluna.  

Uma exibição materializada não pode ser criada em uma tabela com segurança em nível de linha habilitada.

Só é possível criar Exibições Materializadas em tabela particionadas.  Há suporte para a partição SPLIT/MERGE em tabelas base de exibições materializadas; não há suporte para a partição SWITCH.  
 
ALTER TABLE SWITCH não tem suporte em tabelas referenciadas em exibições materializadas. Desabilite ou descarte as exibições materializadas antes de usar ALTER TABLE SWITCH. Nos cenários a seguir, a criação de exibições materializadas requer novas colunas a adicionar à exibição materializada:

|Cenário|Novas colunas a adicionar à exibição materializada|Comentário|  
|-----------------|---------------|-----------------|
|COUNT_BIG() está ausente na lista SELECT de uma definição de exibição materializada| COUNT_BIG (*) |Adicionado automaticamente pela criação da exibição materializada.  Não é necessária nenhuma ação do usuário.|
|SUM(a) é especificado por usuários na lista SELECT de uma definição de exibição materializada E 'a' é uma expressão anulável |COUNT_BIG (a) |Os usuários precisam adicionar a expressão 'a' manualmente na definição de exibição materializada.|
|AVG(a) é especificado por usuários na lista SELECT de uma definição de exibição materializada, em que 'a' é uma expressão.|SUM(a), COUNT_BIG(a)|Adicionado automaticamente pela criação da exibição materializada.  Não é necessária nenhuma ação do usuário.|
|STDEV(a) é especificado por usuários na lista SELECT de uma definição de exibição materializada, em que 'a' é uma expressão.|SUM(a), COUNT_BIG(a), SUM(square(a))|Adicionado automaticamente pela criação da exibição materializada.  Não é necessária nenhuma ação do usuário. |
| | | |

Uma vez criadas, as exibições materializadas são visíveis no SQL Server Management Studio na pasta de exibições da instância do SQL Data Warehouse do Azure.

Os usuários podem executar [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) e [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest) para determinar o espaço que está sendo consumido por uma exibição materializada.  

Uma exibição materializada pode ser descartada por meio de DROP VIEW.  Você pode usar ALTER MATERIALIZED VIEW para desabilitar ou recriar uma exibição materializada.   

O plano EXPLAIN e o gráfico Plano de Execução Estimado no SQL Server Management Studio podem mostrar se o otimizador de consulta considera uma exibição materializada na execução da consulta. e o gráfico Plano de Execução Estimado no SQL Server Management Studio podem mostrar se o otimizador de consulta considera uma exibição materializada na execução da consulta.

Para descobrir se uma instrução SQL pode se beneficiar da nova exibição materializada, execute o comando `EXPLAIN` com `WITH_RECOMMENDATIONS`.  Para obter detalhes, confira [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest).

## <a name="permissions"></a>Permissões

Requer a permissão CREATE VIEW no banco de dados e a permissão ALTER no esquema no qual a exibição está sendo criada. 
  
## <a name="see-also"></a>Confira também

[Ajuste de desempenho com a Exibição Materializada](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[DROP VIEW](/sql/t-sql/statements/drop-view-transact-sql?view=azure-sqldw-latest)  
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Exibições do sistema com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instruções T-SQL com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
