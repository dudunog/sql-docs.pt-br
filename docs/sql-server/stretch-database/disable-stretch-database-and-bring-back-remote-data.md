---
title: Desabilitar Banco de Dados de Stretch e retornar dados remotos
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 80974811f45a88b740aa8d84ea9ac67c2c2c1c07
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73843816"
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>Desabilitar Banco de Dados de Stretch e retornar dados remotos
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para desabilitar o Stretch Database de uma tabela, selecione **Stretch** para uma tabela no SQL Server Management Studio. Então, selecione uma das seguintes opções.  
  
-   **Desabilitar | Trazer de volta os dados do Azure**. Copie os dados remotos da tabela do Azure de volta para o SQL Server, depois desabilite o Stretch Database para a tabela. Essa operação incorre em custos de transferência de dados e não pode ser cancelada.  
  
-   **Desabilitar | Deixar os dados no Azure**. Desabilite o Stretch Database para a tabela.  Abandone os dados remotos da tabela no Azure.  
  
 Você também pode usar o Transact-SQL para desabilitar o Stretch Database de uma tabela ou de um banco de dados.  
  
 Depois de desabilitar o Banco de Dados de Stretch de uma tabela, a migração de dados é interrompida e os resultados da consulta já não incluem os resultados da tabela remota.  
  
 Se você simplesmente deseja pausar a migração de dados, veja [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
> [!NOTE]
> Desabilitar o Stretch Database para uma tabela ou para um banco de dados não exclui o objeto remoto. Se você quiser excluir a tabela remota ou o banco de dados remoto, descarte-o(a) usando o Portal de Gerenciamento do Azure. Os objetos remotos continuam incorrendo em custos do Azure até que você os exclua. Para saber mais, confira [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-table"></a>Desabilitar o Stretch Database para uma tabela  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>Use o SQL Server Management Studio para desabilitar o Stretch Database de uma tabela  
  
1.  No SQL Server Management Studio, no Pesquisador de Objetos, selecione a tabela da qual você deseja desabilitar o Stretch Database.  
  
2.  Clique com o botão direito do mouse e selecione **Stretch**, e escolha uma das opções a seguir.  
  
    -   **Desabilitar | Trazer de volta os dados do Azure**. Copie os dados remotos da tabela do Azure de volta para o SQL Server, depois desabilite o Stretch Database para a tabela. Esse comando não pode ser cancelado.  
  
        > [!NOTE]
        > A cópia dos dados remotos para a tabela do Azure de volta para o SQL Server gera custos de transferência de dados. Para saber mais, confira [Detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
         Depois que todos os dados remotos forem copiados do Azure de volta para o SQL Server, o Stretch será desabilitado para a tabela.  
  
    -   **Desabilitar | Deixar os dados no Azure**. Desabilite o Stretch Database para a tabela.  Abandone os dados remotos da tabela no Azure.  
  
    > [!NOTE]
    > Desabilitar o Stretch Database de uma tabela não exclui os dados remotos ou a tabela remota. Se você quiser excluir a tabela remota, descarte-a usando o Portal de Gerenciamento do Azure. A tabela remota continua a gerar custos do Azure até você excluí-la. Para saber mais, confira [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>Usar o Transact-SQL para desabilitar o Stretch Database de uma tabela.  
  
-   Para desabilitar o Stretch de uma tabela e copiar os dados remotos referente à tabela do Azure de volta para o SQL Server, execute o comando a seguir. Depois que todos os dados remotos forem copiados do Azure de volta para o SQL Server, o Stretch será desabilitado para a tabela.

    Esse comando não pode ser cancelado.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > A cópia dos dados remotos para a tabela do Azure de volta para o SQL Server gera custos de transferência de dados. Para saber mais, confira [Detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/).    
  
-   Para desabilitar o Stretch de uma tabela e abandonar os dados remotos, execute o comando a seguir.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> Desabilitar o Stretch Database de uma tabela não exclui os dados remotos ou a tabela remota. Se você quiser excluir a tabela remota, descarte-a usando o Portal de Gerenciamento do Azure. A tabela remota continua a gerar custos do Azure até você excluí-la. Para saber mais, confira [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-database"></a>Desabilitar o Banco de Dados de Stretch para um banco de dados  
 Antes de desabilitar o Stretch Database para um banco de dados, você precisa desabilitar o Stretch Database em tabelas individuais habilitadas para Stretch no banco de dados.  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>Usar o SQL Server Management Studio para desabilitar o Banco de Dados de Stretch para um banco de dados  
  
1.  No SQL Server Management Studio, no Pesquisador de Objetos, selecione o banco de dados do qual você deseja desabilitar o Stretch Database.  
  
2.  Clique com o botão direito do mouse e selecione **Tarefas**, **Stretch**e **Desabilitar**.  
  
> [!NOTE]
> Desabilitar o Stretch Database de um banco de dados não exclui o banco de dados remoto. Se deseja excluir o banco de dados remoto, você deve descartá-la usando o Portal de Gerenciamento do Azure. O banco de dados remoto continua a gerar custos do Azure até você excluí-la. Para saber mais, confira [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>Usar o Transact-SQL para desabilitar o Stretch Database de um banco de dados.  
 Execute o comando a seguir.  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> Desabilitar o Stretch Database de um banco de dados não exclui o banco de dados remoto. Se deseja excluir o banco de dados remoto, você deve descartá-la usando o Portal de Gerenciamento do Azure. O banco de dados remoto continua a gerar custos do Azure até você excluí-la. Para saber mais, confira [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="see-also"></a>Consulte Também  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
