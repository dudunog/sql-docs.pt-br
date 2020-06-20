---
title: Preencher índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9ab93a3514fa260c8c3836da85c767da3c3051a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004059"
---
# <a name="populate-full-text-indexes"></a>Popular índices de texto completo
  A criação e a manutenção de um índice de texto completo envolvem popular o índice usando um processo chamado *população* (também conhecido como *rastreamento*).  
  
##  <a name="types-of-population"></a><a name="types"></a>Tipos de população  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o dá suporte aos seguintes tipos de população: população completa, população automática baseada em controle de alterações ou preenchimento manual e população incremental baseada em carimbo de data/hora.  
  
### <a name="full-population"></a>População completa  
 Durante uma população completa, entradas de índice são criadas para todas as linhas de uma tabela ou exibição indexada. Uma população completa de um índice de texto completo cria entradas de índice para todas as linhas da tabela base ou da exibição indexada.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popula totalmente um novo índice de texto completo assim que ele é criado. No entanto, uma população completa pode consumir recursos consideráveis. Portanto, quando você criar um índice de texto completo durante períodos de pico, uma prática recomendada será atrasar a população completa até uma hora fora do horário de pico, principalmente se a tabela base de um índice de texto completo for grande. Todavia, o catálogo de texto completo ao qual o índice pertence não poderá ser utilizado até que todos os índices de texto completo estejam populados. Para criar um índice de texto completo sem populá-lo imediatamente, especifique a cláusula CHANGE_TRACKING OFF, NO POPULATION na instrução CREATE FULLTEXT INDEX. Se você especificar CHANGE_TRACKING MANUAL, o Mecanismo de Texto Completo usará a instrução. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o não preencherá o novo índice de texto completo até que você execute uma instrução ALTER FULLTEXT INDEX usando a cláusula iniciar população completa ou iniciar população INCREMENTAL. Para obter mais informações, consulte os exemplos “A. Criando um índice de texto completo sem executar uma população completa" e "B. Executando uma população completa em tabela", mais adiante neste tópico.  
  

  
### <a name="change-tracking-based-population"></a>População com base em controle de alterações  
 Como opção, você pode usar o controle de alterações para manter um índice de texto completo após a população completa inicial. Há uma pequena sobrecarga associada ao controle de alterações porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém uma tabela em que controla as alterações feitas na tabela base desde a última população. Quando é usado o controle de alterações, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém um registro das linhas da tabela base ou exibição indexada que foram modificadas por atualizações, exclusões ou inserções. As alterações de dados por meio de WRITETEXT e UPDATETEXT não são refletidas no índice de texto completo e não são coletadas com o controle de alterações.  
  
> [!NOTE]  
>  Para tabelas que contêm uma coluna `timestamp`, você pode usar populações incrementais.  
  
 Quando o controle de alterações é habilitado durante a criação do índice, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popula completamente o novo índice de texto completo logo após sua criação. Consequentemente, as alterações são controladas e propagadas para o índice de texto completo. Há dois tipos de controle de alterações: automático (opção CHANGE_TRACKING AUTO) e manual (opção CHANGE_TRACKING MANUAL). O controle de alterações automático é o comportamento padrão.  
  
 O tipo de controle de alterações determina como o índice de texto completo é populado, como segue:  
  
-   População automática  
  
     Por padrão, ou se você especificar CHANGE_TRACKING AUTO, o Mecanismo de Texto Completo usa população automática no índice de texto completo. Depois que a população completa inicial é concluída, as alterações são controladas à medida que os dados são modificados na tabela base, e as alterações controladas são propagadas automaticamente. O índice de texto completo é atualizado em segundo plano, mas as alterações propagadas podem não ser refletidas imediatamente no índice.  
  
     **Para configurar o controle de alterações com população automática**  
  
    -   [criar índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... COM CHANGE_TRACKING AUTOMÁTICO  
  
    -   [alterar índice de texto completo](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... DEFINIR CHANGE_TRACKING AUTOMATICAMENTE  
  
     Para obter mais informações, consulte o exemplo “E. Alterando um índice de texto completo para usar o controle de alterações automáticas”, mais adiante neste tópico.  
  
-   População manual  
  
     Se você especificar CHANGE_TRACKING MANUAL, o Mecanismo de Texto Completo usará população manual no índice de texto completo. Depois que a população completa inicial é concluída, as alterações são controladas à medida que os dados são modificados na tabela base. No entanto, eles não são propagados para o índice de texto completo até que você execute um ALTER FULLTEXT INDEX... Instrução START UPDATE population. É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para chamar essa instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] periodicamente.  
  
     **Para começar a controlar alterações com população manual**  
  
    -   [criar índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... COM CHANGE_TRACKING MANUAL  
  
    -   [alterar índice de texto completo](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... DEFINIR CHANGE_TRACKING MANUAL  
  
     Para obter mais informações, consulte o exemplo “C. Criando um índice de texto completo com controle de alterações manual" e "D. Executando uma população manual", posteriormente neste tópico.  
  
 **Para desativar o rastreamento de alterações**  
  
-   [criar índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... COM CHANGE_TRACKING DESATIVADO  
  
-   [alterar índice de texto completo](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... DEFINIR CHANGE_TRACKING DESATIVADO  
  

  
### <a name="incremental-timestamp-based-population"></a>População incremental baseada em carimbo de data e hora  
 Uma população incremental é um mecanismo alternativo para popular um índice de texto completo manualmente. Você pode executar uma população incremental para um índice de texto completo que tem CHANGE_TRACKING definido como MANUAL ou OFF. Se a primeira população em um índice de texto completo for uma população incremental, ele indexará todas as linhas, tornando-a equivalente a uma população completa.  
  
 O requisito para população incremental é que a tabela indexada deve ter uma coluna do tipo de dados `timestamp`. Se uma coluna `timestamp` não existir, a população incremental não poderá ser executada. Uma solicitação para população incremental em uma tabela sem uma coluna `timestamp` resulta em uma operação de população completa. Além disso, se nenhum metadado que afeta o índice de texto completo da tabela foi alterado desde a última população, as solicitações de população incremental serão implementadas como populações completas. Isso inclui alterações de metadados geradas pela alteração de qualquer coluna, índice ou definições de índice de texto completo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a coluna `timestamp` para identificar linhas que foram alteradas desde a última população. A população incremental então atualiza o índice de texto completo com linhas adicionadas, excluídas ou modificadas após a última população ou enquanto a última população estava em andamento. Se uma tabela tiver um volume alto de inserções, usar a população incremental poderá ser mais eficiente do que usar a população manual.  
  
 Ao término de uma população, o Mecanismo de Texto Completo registra um novo valor de `timestamp`. Esse valor é o maior valor de `timestamp` que o SQL Gatherer encontrou. Esse valor será usado quando uma população incremental subsequente for iniciada.  
  
 Para executar uma população incremental, execute uma instrução ALTER FULLTEXT INDEX usando a cláusula START INCREMENTAL POPULATION.  
  

  
##  <a name="examples-of-populating-full-text-indexes"></a><a name="examples"></a>Exemplos de preenchimento de índices de texto completo  
  
> [!NOTE]  
>  Os exemplos desta seção usam a tabela `Production.Document` ou `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` .  
  
### <a name="a-creating-a-full-text-index-without-running-a-full-population"></a>a. Criando um índice de texto completo sem executar uma população completa  
 O exemplo a seguir cria um índice de texto completo na tabela `Production.Document` do banco de dados de exemplo `AdventureWorks` . Este exemplo usa WITH CHANGE_TRACKING OFF, NO POPULATION para atrasar a população completa inicial.  
  
```  
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="b-running-a-full-population-on-table"></a>B. Executando uma população completa em tabela  
 O exemplo a seguir executa uma população completa na tabela `Production.Document` do banco de dados de exemplo `AdventureWorks` .  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### <a name="c-creating-a-full-text-index-with-manual-change-tracking"></a>C. Criando um índice de texto completo com controle de alterações manuais  
 O exemplo a seguir cria um índice de texto completo que usará o controle de alterações com população manual na tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` .  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### <a name="d-running-a-manual-population"></a>D. Executando uma população manual  
 O exemplo a seguir executa uma população manual no índice de texto completo com controle de alterações da tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` .  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### <a name="e-altering-a-full-text-index-to-use-automatic-change-tracking"></a>E. Alterando um índice de texto completo para usar o controle de alterações automáticas  
 O exemplo a seguir altera o índice de texto completo da tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` para usar o controle de alterações com população automática.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  

  
##  <a name="creating-or-changing-a-schedule-for-incremental-population"></a><a name="create"></a>Criando ou alterando uma agenda para população incremental  
  
#### <a name="to-create-or-change-a-schedule-for-incremental-population-in-management-studio"></a>Para criar ou alterar uma agenda para população incremental no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e expanda o banco de dados que contém o índice de texto completo.  
  
3.  Expanda **Tabelas**.  
  
 Clique com o botão direito do mouse na tabela em que o índice de texto completo está definido, selecione **Índice de Texto Completo**e, no menu de contexto **Índice de Texto Completo** , clique em **Propriedades**. Este procedimento abre a caixa de diálogo **Propriedades do Índice de Texto Completo** .  
  
1.  No painel **selecionar uma página** , selecione agendas.  
  
     Use esta página para criar ou gerenciar agendas para um trabalho do SQL Server Agent que inicia uma população incremental de tabela na tabela base ou na exibição indexada do índice de texto completo.  
  
    > [!IMPORTANT]  
    >  Se a tabela base ou a exibição não contiver uma coluna do tipo de dados `timestamp`, uma população completa será executada.  
  
     As opções são as descritas a seguir:  
  
    -   Para criar uma nova agenda, clique em **Novo**.  
  
         Este procedimento abre a caixa de diálogo **Novo Agendamento da Tabela de Indexação de Texto Completo** , em que é possível criar um agendamento. Para salvar o agendamento, clique em **OK**.  
  
        > [!IMPORTANT]  
        >  Um trabalho do SQL Server Agent (Iniciar População Incremental da Tabela em *database_name*.*table_name*) é associado a um novo agendamento depois que você sai da caixa de diálogo **Propriedades do Índice de Texto Completo** . Se você criar várias agendas para o índice de texto completo, todos eles usarão o mesmo trabalho.  
  
    -   Para alterar um agendamento, selecione-o e clique em **Editar**.  
  
         Este procedimento abre a caixa de diálogo **Novo Agendamento da Tabela de Indexação de Texto Completo** , em que é possível modificar o agendamento.  
  
        > [!NOTE]  
        >  Para obter informações sobre como modificar um trabalho, veja [Modificar um trabalho](../../ssms/agent/modify-a-job.md).  
  
    -   Para remover um agendamento, selecione-o e clique em **Excluir**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  

  
##  <a name="troubleshooting-errors-in-a-full-text-population-crawl"></a><a name="crawl"></a>Solucionando problemas de erros em uma população de texto completo (rastreamento)  
 Quando um erro ocorrer durante um rastreamento, o recurso de registro de rastreamento de pesquisa de texto completo cria e mantém um log de rastreamento, que é um texto sem-formatação. Cada log de rastreamento corresponde a um catálogo de texto completo específico. Por padrão, os logs de rastreamento para uma determinada instância, neste caso, a primeira instância, estão localizados na pasta %Arquivos de programas%\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG. O arquivo de log de rastreamento segue o seguinte esquema de nomeação:  
  
 SQLFT \<DatabaseID> \<FullTextCatalogID> . LOG [ \<n> ]  
  
 <`DatabaseID`>  
 A ID de um banco de dados. <`dbid`> é um número de cinco dígitos com zeros à esquerda.  
  
 <`FullTextCatalogID`>  
 ID do catálogo de texto completo. <`catid`> é um número de cinco dígitos com zeros à esquerda.  
  
 <`n`>  
 É um inteiro que indica um ou mais logs de rastreamento que existem do mesmo catálogo de texto completo.  
  
 Por exemplo, SQLFT0000500008.2 é o arquivo de log de rastreamento para o banco de dados com o ID de banco de dados = 5 e ID de catálogo de texto completo = 8. O 2 no final do nome do arquivo indica que há dois arquivos de log de rastreamento para esse par de banco de dados/catálogo.  
  

  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)   
 [Iniciar a pesquisa de texto completo](get-started-with-full-text-search.md)   
 [Criar e gerenciar índices de texto completo](create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
