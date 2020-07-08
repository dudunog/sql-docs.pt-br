---
title: Habilitar índices e restrições | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32d0516d8f3227a3fbf18d8649b0a79bdd60c790
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85629625"
---
# <a name="enable-indexes-and-constraints"></a>Habilitar índices e restrições
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico descreve como habilitar um índice desabilitado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Depois que um índice for desabilitado, ele permanecerá em estado desabilitado até que seja recriado ou descartado  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para habilitar um índice desabilitado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Depois da reconstrução do índice, qualquer restrição que tiver sido desabilitada devido à desabilitação do índice deverá ser habilitada manualmente. As restrições PRIMARY KEY e UNIQUE são habilitadas reconstruindo o índice associado. Esse índice deve ser reconstruído (habilitado) antes de você poder habilitar restrições FOREIGN KEY que fazem referência à restrição PRIMARY KEY ou UNIQUE. Restrições FOREIGN KEY são habilitadas usando a instrução ALTER TABLE CHECK CONSTRAINT.  
  
-   A recriação de um índice clusterizado desabilitado não pode ser efetuada quando a opção ONLINE está definida como ON.  
  
-   Quando o índice clusterizado é habilitado ou desabilitado e o índice não clusterizado é desabilitado, a ação do índice clusterizado tem os seguintes resultados no índice não clusterizado desabilitado.  
  
    |Ação de índice clusterizado|Índice não clusterizado desabilitado...|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD.|Permanece desabilitado.|  
    |ALTER INDEX ALL REBUILD.|É reconstruído e habilitado.|  
    |DROP INDEX.|Permanece desabilitado.|  
    |CREATE INDEX WITH DROP_EXISTING.|Permanece desabilitado.|  
  
     A criação de um novo índice clusterizado se comporta da mesma forma que ALTER INDEX ALL REBUILD.  
  
-   Ações permitidas em índices não clusterizados associados a um índice clusterizado dependem do estado, se desabilitado ou habilitado, de ambos os tipos de índice. A tabela a seguir resume as ações permitidas em índices não clusterizados.  
  
    |Ação de índice não clusterizado|Quando os índices clusterizados e não clusterizados estão desabilitados.|Quando o índice clusterizado está habilitado e o índice não clusterizado está em um dos estados.|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD.|A ação falha.|A ação tem êxito.|  
    |DROP INDEX.|A ação tem êxito.|A ação tem êxito.|  
    |CREATE INDEX WITH DROP_EXISTING.|A ação falha.|A ação tem êxito.|  

-   Quando a recompilação desabilitar os índices não clusterizados compactados, data_compression usará “none” como padrão, o que significa que os índices serão descompactados. Isso ocorre devido à perda dos metadados das configurações de compactação quando os índices não clusterizados são desabilitados. Para resolver esse problema, é necessário especificar a compactação de dados explícita na instrução de recompilação.

###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. Se estiver usando o DBCC DBREINDEX, o usuário deverá ter a tabela ou ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enable-a-disabled-index"></a>Para habilitar um índice desabilitado  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja habilitar um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja habilitar um índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser habilitado e selecione **Recriar**.  
  
6.  Na caixa de diálogo **Recriar Índices** , verifique se o índice correto está na grade **Índices a serem recriados** e clique em **OK**.  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>Para habilitar todos os índices de uma tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja habilitar os índices.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja habilitar os índices.  
  
4.  Clique com o botão direito do mouse na pasta **Índices** e selecione **Recriar Tudo**.  
  
5.  Na caixa de diálogo **Recriar Índices** , verifique se os índices corretos estão na grade **Índices a serem recriados** e clique em **OK**. Para remover um índice da grade **Índices a serem recriados** , selecione o índice e pressione a tecla Delete.  
  
 As seguintes informações estão disponíveis na caixa de diálogo **Recriar Índices** :  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>Para habilitar um índice desabilitado usando ALTER INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>Para habilitar um índice desabilitado usando CREATE INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>Para habilitar um índice desabilitado usando DBCC DBREINDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>Para habilitar todos os índices em uma tabela usando ALTER INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>Para habilitar todos os índices em uma tabela usando DBCC DBREINDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md), [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) e [DBCC DBREINDEX &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md).  
  
  
