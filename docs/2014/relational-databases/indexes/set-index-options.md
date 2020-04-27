---
title: Definir opções de índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24587f27710381ac787fe8045029df681e401af5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63036186"
---
# <a name="set-index-options"></a>Opções Set Index
  Este tópico descreve como modificar as propriedades de um índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar as propriedades de um índice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   As opções a seguir são se aplicadas imediatamente ao índice usando a cláusula SET na instrução ALTER INDEX: ALLOW_PAGE_LOCKS, ALLOW_ROW_LOCKS, IGNORE_DUP_KEY e STATISTICS_NORECOMPUTE.  
  
-   As seguintes opções podem ser definidas quando você recompila um índice usando ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING: PAD_INDEX, FILLFACTOR, SORT_IN_TEMPDB, IGNORE_DUP_KEY, STATISTICS_NORECOMPUTE, ONLINE, ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, MAXDOP e DROP_EXISTING (somente CREATE INDEX).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>Para modificar as propriedades de um índice no Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você modificar as propriedades de um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela em que você deseja modificar as propriedades de um índice e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
5.  Selecione o índice a ser modificado. Suas propriedades aparecerão na grade principal.  
  
6.  Altere as configurações de alguma ou de todas as propriedades para personalizar o índice.  
  
7.  Clique em **fechar**  
  
8.  No menu **Arquivo** , selecione **Salvar**_table_name_.  
  
#### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>Para modificar as propriedades de um índice no Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você modificar as propriedades de um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja modificar as propriedades do índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice cujas propriedades serão modificadas e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Opções**.  
  
7.  Altere as configurações de alguma ou de todas as propriedades para personalizar o índice.  
  
8.  Para adicionar, remover ou alterar a posição de uma coluna de índice, selecione a página **Geral** na caixa de diálogo **Propriedades do Índice –** _nome_do_índice_. Para obter mais informações, consulte [Index Properties F1 Help](index-properties-f1-help.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>Para ver as propriedades de todos os índices em uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT i.name AS index_name,   
        i.type_desc,   
        i.is_unique,   
        ds.type_desc AS filegroup_or_partition_scheme,   
        ds.name AS filegroup_or_partition_scheme_name,   
        i.ignore_dup_key,   
        i.is_primary_key,   
        i.is_unique_constraint,   
        i.fill_factor,   
        i.is_padded,   
        i.is_disabled,   
        i.allow_row_locks,   
        i.allow_page_locks,   
        i.has_filter,   
        i.filter_definition  
    FROM sys.indexes AS i  
       INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
    WHERE is_hypothetical = 0 AND i.index_id <> 0   
       AND i.object_id = OBJECT_ID('HumanResources.Employee');   
    GO  
  
    ```  
  
#### <a name="to-set-the-properties-of-an-index"></a>Para definir as propriedades de um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta e clique em **Executar**.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
  
