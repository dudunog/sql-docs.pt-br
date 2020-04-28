---
title: Reorganizar e recompilar índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.fragmentation.f1
- sql12.swb.index.reorg.f1
- sql12.swb.index.rebuild.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8c1c78e1d126420b17a1b8de0499c432059b25ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68811033"
---
# <a name="reorganize-and-rebuild-indexes"></a>Reorganizar e recriar índices
  Este tópico descreve como reorganizar ou recompilar índice fragmentado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mantém os índices automaticamente sempre que são realizadas operações de entrada, atualização ou exclusão nos dados subjacentes. No decorrer do tempo, essas modificações podem fazer com que as informações do índice sejam dispersadas pelo banco de dados (fragmentadas). A fragmentação ocorre quando os índices têm páginas nas quais a ordem lógica, com base no valor de chave, não corresponde à ordem física do arquivo de dados. Índices com fragmentação pesada podem degradar o desempenho da consulta e causar lentidão de resposta do aplicativo.  
  
 Você pode solucionar a fragmentação de índice reorganizando ou recriando um índice. Para índices particionados criados em um esquema de partição, é possível usar qualquer um desses métodos em um índice completo ou em uma única partição de índice. A recriação de um índice descarta e recria o índice. Isso remove a fragmentação, recupera espaço em disco ao compactar as páginas com base na configuração do fator de preenchimento especificada ou existente, e reclassifica as linhas do índice em páginas contíguas. Quando ALL é especificado, todos os índices da tabela são descartados e recriados em uma única transação. A reorganização de um índice utiliza recursos mínimos do sistema. Ela desfragmenta o nível folha de índices clusterizados e não clusterizados em tabelas e exibições, reordenando fisicamente as páginas de nível folha para que correspondam à ordem lógica, da esquerda para a direita, dos nós folha. A reorganização também compacta as páginas de índice. A compactação baseia-se no valor do fator de preenchimento existente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Detectando a fragmentação](#Fragmentation)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para verificar a fragmentação de um índice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureFrag)  
  
     [Transact-SQL](#TsqlProcedureFrag)  
  
-   **Para reorganizar ou recompilar um índice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureReorg)  
  
     [Transact-SQL](#TsqlProcedureReorg)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="detecting-fragmentation"></a><a name="Fragmentation"></a>Detectando a fragmentação  
 A primeira etapa para optar pelo método de fragmentação a ser usado é analisar o índice para determinar o grau de fragmentação. Usando a função de sistema [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql), você pode detectar a fragmentação em um índice específico, em todos os índices de uma tabela ou exibição indexada, em todos os índices de um banco de dados ou em todos os índices de todos os bancos de dados. Para índices particionados, **sys.dm_db_index_physical_stats** também fornece informações de fragmentação por partição.  
  
 O conjunto de resultados retornado pela função **sys.dm_db_index_physical_stats** inclui as colunas a seguir.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|Porcentagem de fragmentação lógica (páginas fora de ordem no índice).|  
|**fragment_count**|Número de fragmentos (páginas folha fisicamente consecutivas) do índice.|  
|**avg_fragment_size_in_pages**|Número médio de páginas em um fragmento de índice.|  
  
 Depois que o grau de fragmentação for conhecido, use a tabela a seguir para determinar o melhor método para corrigir a fragmentação.  
  
|Valor**avg_fragmentation_in_percent**|Instrução corretiva|  
|-----------------------------------------------|--------------------------|  
|> 5% e \< = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> A recompilação de um índice pode ser executada online ou offline. A reorganização de um índice sempre é executada online. Para atingir disponibilidade semelhante à opção de reorganização, recrie índices online.  
  
> [!TIP]
> Esses valores fornecem uma orientação aproximada para determinar o ponto em que você deve mudar entre `ALTER INDEX REORGANIZE` e `ALTER INDEX REBUILD`. Contudo, os valores reais podem variar de acordo com o caso. É importante que você experimente para poder determinar o melhor limite para um ambiente. Por exemplo, se um determinado índice for usado principalmente para operações de verificação, o desempenho delas poderá ser aprimorado pela remoção da fragmentação. O benefício de desempenho é menos perceptível para índices que são usados principalmente para operações de busca. Da mesma forma, remover a fragmentação em um heap (uma tabela sem índice clusterizado) é especialmente útil para operações de verificação de índice não clusterizado, mas tem pouco efeito em operações de pesquisa.

Em geral, níveis muito baixos de fragmentação (menos de 5 por cento) não devem ser resolvidos por nenhum desses comandos, pois o benefício da remoção de uma pequena quantidade de fragmentação é quase sempre amplamente excedido pelo custo da reorganização ou da recriação do índice. 

> [!NOTE]
> A recriação ou reorganização de índices pequenos geralmente não reduz a fragmentação. As páginas de índices pequenos às vezes são armazenadas em extensões mistas. Extensões mistas são compartilhadas por até oito objetos, portanto, a fragmentação em um índice pequeno pode não ser reduzida após a reorganização ou recriação.

### <a name="index-defragmentation-considerations"></a>Considerações sobre fragmentação de índice
Em determinadas condições, recompilar um índice clusterizado recompilará automaticamente todo índice não clusterizado que faça referência à chave de clustering, se os identificadores físicos ou lógicos contidos nos registros de índice não clusterizados precisarem ser alterados.

Cenários que requerem que todos os índices não clusterizados sejam automaticamente recompilados em uma tabela:

-  Criar um índice clusterizado em uma tabela
-  Remover um índice clusterizado, fazendo com que a tabela seja armazenada como um heap
-  Alterar a chave de clustering para incluir ou excluir colunas

Cenários que não requerem que todos os índices não clusterizados sejam automaticamente recompilados em uma tabela:

-  Recompilar um índice clusterizado exclusivo
-  Recompilar um índice clusterizado não exclusivo
-  Alterar o esquema de índice (assim como ao aplicar um esquema de particionamento a um índice clusterizado) ou mover o índice clusterizado para um grupo de arquivos diferente
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
Índices com mais de 128 extensões são recriados em duas fases separadas: lógica e física. Na fase lógica, as unidades de alocação existentes usadas pelo índice são marcadas para desalocação, as linhas de dados são copiadas, ordenadas e, depois, movidas para novas unidades de alocação criadas para armazenar o índice recriado. Na fase física, as unidades de alocação previamente marcadas para desalocação são fisicamente canceladas em transações curtas que ocorrem em segundo plano e que não exigem muitos bloqueios. Para obter mais informações sobre as extensões, consulte o [Guia de arquitetura de páginas e extensões](https://docs.microsoft.com/sql/relational-databases/pages-and-extents-architecture-guide).

A instrução `ALTER INDEX REORGANIZE` exige que o arquivo de dados que contém o índice tenha espaço disponível, pois a operação só pode alocar páginas de trabalho temporárias no mesmo arquivo, não em outro arquivo no grupo de arquivos. Portanto, embora o grupo de arquivos possa ter páginas livres disponíveis, o usuário ainda poderá se deparar com o erro 1105:`Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

É possível criar e recompilar índices não alinhados em uma tabela com mais de 1.000 partições, mas isso não é recomendado. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações.

Um índice não poderá ser reorganizado ou recriado se o grupo de arquivos no qual ele está localizado estiver offline ou definido como somente leitura. Quando a palavra-chave `ALL` for especificada e um ou mais índices estiver em um grupo de arquivos offline ou somente leitura, a instrução falhará.
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão `ALTER` na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedureFrag"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Para verificar a fragmentação de um índice  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja verificar a fragmentação de um índice.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja verificar a fragmentação de um índice.  
  
4.  Expanda a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice cuja fragmentação você deseja verificar e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Fragmentação**.  
  
     As informações a seguir estão disponíveis na página **Fragmentação** :  
  
     **Preenchimento da página**  
     Indica o preenchimento médio das páginas do índice, como uma porcentagem. 100% significa que as páginas de índice estão completamente preenchidas. 50% significa que, em média, cada página do índice está preenchida pela metade.  
  
     **Fragmentação total**  
     A porcentagem de fragmentação lógica. Isso indica o número de páginas em um índice que não estão armazenadas em ordem.  
  
     **Tamanho médio da linha**  
     O tamanho médio de uma linha de nível folha.  
  
     **Profundidade**  
     O número de níveis no índice, inclusive o nível folha.  
  
     **Registros encaminhados**  
     O número de registros em um heap com ponteiros encaminhados a outro local de dados (Esse estado ocorre durante uma atualização, quando não há espaço suficiente para armazenar a nova linha no local original.)  
  
     **Linhas fantasmas**  
     O número de linhas que estão marcadas como excluídas, mas ainda não foram removidas. Essas linhas serão removidas por um thread de limpeza, quando o servidor não estiver ocupado. Esse valor não inclui linhas que estejam sendo retidas devido a uma transação de isolamento de instantâneo pendente.  
  
     **Tipo de índice**  
     O tipo do índice. Os valores possíveis são **Índice cluster**, **Índice não cluster**e **XML Primário**. As tabelas também podem ser armazenadas como um heap (sem-índices), mas nesse caso a página Propriedades do Índice não pode ser aberta.  
  
     **Linhas em nível folha**  
     O número de linhas em nível folha.  
  
     **Tamanho máximo da linha**  
     O tamanho máximo da linha em nível folha.  
  
     **Tamanho mínimo da linha**  
     O tamanho mínimo da linha em nível folha.  
  
     **Páginas**  
     O número total de páginas de dados.  
  
     **Partition ID**  
     A ID da partição da árvore b que contém o índice.  
  
     **Linhas fantasmas de versão**  
     O número de registros fantasmas que estão sendo retidos devido a uma transação de isolamento de instantâneo pendente.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedureFrag"></a> Usando o Transact-SQL  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Para verificar a fragmentação de um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     A instrução acima poderia retornar um conjunto de resultados semelhante ao que segue.  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
 Para obter mais informações, consulte [Sys. dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedureReorg"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>Para reorganizar ou recriar um índice  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar um índice.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja reorganizar um índice.  
  
4.  Expanda a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser reorganizado e selecione **Reorganizar**.  
  
6.  Na caixa de diálogo **Reorganizar Índices** , verifique se o índice correto está na grade **Índices a serem reorganizados** e clique em **OK**.  
  
7.  Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.  
  
8.  Clique em **OK**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos os índices de uma tabela  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar os índices.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja reorganizar os índices.  
  
4.  Clique com o botão direito do mouse na pasta **Índices** e selecione **Reorganizar Tudo**.  
  
5.  Na caixa de diálogo **Reorganizar Índices** , verifique se os índices corretos estão na grade **Índices a serem reorganizados**e clique em OK. Para remover um índice da grade **Índices a serem reorganizados** , selecione o índice e pressione a tecla Delete.  
  
6.  Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.  
  
7.  Clique em **OK**  
  
#### <a name="to-rebuild-an-index"></a>Para recriar um índice  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar um índice.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja reorganizar um índice.  
  
4.  Expanda a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser reorganizado e selecione **Reorganizar**.  
  
6.  Na caixa de diálogo **Recriar Índices** , verifique se o índice correto está na grade **Índices a serem recriados** e clique em **OK**.  
  
7.  Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.  
  
8.  Clique em **OK**  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedureReorg"></a> Usando o Transact-SQL  
  
#### <a name="to-reorganize-a-defragmented-index"></a>Para reorganizar um índice desfragmentado  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos os índices de uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-defragmented-index"></a>Para recriar um índice desfragmentado  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo recria um único índice na tabela `Employee` .  
  
     [!code-sql[IndexDDL#AlterIndex1](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex1)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>Para recriar todos os índices de uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na consulta. O exemplo especifica a palavra-chave `ALL`. Isso recria todos os índices associados à tabela. Três opções são especificadas.  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Práticas recomendadas de desfragmentação de índice do Microsoft SQL Server 2000](https://technet.microsoft.com/library/cc966523.aspx)  
  
  
