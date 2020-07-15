---
title: Conectar e consultar um Banco de Dados SQL do Azure
description: Este guia de início rápido mostra como usar o Azure Data Studio para conectar-se a um Banco de Dados SQL e executar uma consulta
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu; maghan; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; sqlfreshmay19; seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: 73e910b6d199a4918eafca067a95136e31ac079c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771959"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-azure-sql-database"></a>Início Rápido: use o Azure Data Studio para se conectar e consultar e o Banco de Dados SQL do Azure

Neste guia de início rápido, você usará o Azure Data Studio para conectar-se a um servidor do Banco de Dados SQL do Azure. Em seguida, executará instruções T-SQL (Transact-SQL) para criar e consultar o banco de dados TutorialDB, que é usado em outros tutoriais do Azure Data Studio.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este guia de início rápido, você precisa do Azure Data Studio e do servidor do Banco de Dados SQL do Azure.

- [Instalar o Azure Data Studio](download.md)

Se você não tiver um SQL Server do Azure, conclua um dos seguintes guias de início rápido do Banco de Dados SQL do Azure. Lembre-se do nome do servidor totalmente qualificado e das credenciais de entrada para etapas posteriores:

- [Criar BD – Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Criar BD – CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Criar BD – PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectar-se a seu servidor do Banco de Dados SQL do Azure

Use o Azure Data Studio para estabelecer uma conexão com o servidor do Banco de Dados SQL do Azure.

1. Na primeira vez que você executar o Azure Data Studio, a página **inicial** deverá abrir. Se você não vir a página **Bem-vindo**, selecione **Ajuda** > **Bem-vindo**. Selecione **Nova Conexão** para abrir o painel de **Conexão**:
   
   ![Ícone de Nova Conexão](media/quickstart-sql-database/new-connection-icon.png)

2. Este artigo usa a entrada do SQL, mas também é compatível com a autenticação do Windows. Preencha os campos a seguir usando o nome do servidor, o nome de usuário e a senha para seu SQL Server do Azure:

   | Configuração       | Valor sugerido | Descrição |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Algo como: **servername.database.windows.net**. |
   | **Autenticação** | Logon do SQL| Este tutorial usa a autenticação do SQL. |
   | **Nome de usuário** | O nome de usuário da conta do administrador do servidor | O nome de usuário da conta usada para criar o servidor. |
   | **Senha (Logon do SQL)** | A senha da conta do administrador do servidor | A senha da conta usada para criar o servidor. |
   | **Salvar senha?** | Sim ou não | Selecione **Sim** se você não quiser inserir a senha a cada vez. |
   | **Nome do banco de dados** | *deixar em branco* | Você está se conectando apenas ao servidor aqui. |
   | **Grupo de Servidores** | Selecione <Default> | Você pode definir esse campo para um grupo de servidores específico que você criou. | 

   ![Ícone de Nova Conexão](media/quickstart-sql-database/new-connection-screen.png)  

3. Selecione **Conectar**.

4. Se o servidor não tiver uma regra de firewall que permita que o Azure Data Studio se conecte, o formulário **Criar nova regra de firewall** será aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, confira [Regras de firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-database/firewall.png)  

Depois de se conectar com êxito, o servidor será aberto na barra lateral **SERVIDORES**.

## <a name="create-the-tutorial-database"></a>Criar o banco de dados do tutorial

As seções a seguir criam o banco de dados TutorialDB que é usado em outros tutoriais do Azure Data Studio.

1. Clique com o botão direito do mouse no SQL Server do Azure na barra lateral **SERVIDORES** e selecione **Nova Consulta**.

1. Cole esse SQL no editor de consultas.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. Na barra de ferramentas, selecione **Executar**. As notificações aparecem no painel **MENSAGENS** mostrando o progresso da consulta.

## <a name="create-a-table"></a>Criar uma tabela

O editor de consultas está conectado ao banco de dados **mestre**, mas queremos criar uma tabela no banco de dados **TutorialDB**. 

1. Conecte-se ao banco de dados **TutorialDB**.

   ![Alterar contexto](media/quickstart-sql-database/change-context2.png)



1. Crie uma tabela `Customers`. 

   Substitua a consulta anterior no editor de consultas por esta e selecione **Executar**.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>Inserir linhas na tabela

Substitua a consulta anterior por esta e selecione **Executar**.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>Exibir o resultado

Substitua a consulta anterior por esta e selecione **Executar**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Os resultados da consulta são exibidos:

   ![Selecionar resultados](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Limpar os recursos

Artigos de início rápido posteriores desenvolvem os recursos criados aqui. Se você planeja trabalhar com esses artigos, não exclua esses recursos. Caso contrário, no portal do Azure, exclua os recursos de que não precisa mais. Para obter detalhes, confira [Limpar recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito a um Banco de Dados SQL do Azure e executou uma consulta, experimente o [Tutorial do editor de código](tutorial-sql-editor.md).
