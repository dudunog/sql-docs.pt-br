---
title: Conectar-se a uma instância do SQL Server e consultá-la usando o SSMS (SQL Server Management Studio)
description: Conecte-se a uma instância do SQL Server no SSMS. Crie e consulte um banco de dados do SQL Server no SSMS executando consultas T-SQL básicas.
ms.prod: sql
ms.technology: ssms
ms.topic: quickstart
author: markingmyname
ms.author: maghan
ms.reviewer: sstein, mikeray
ms.custom: contperf-fy21q2
ms.date: 12/15/2020
ms.openlocfilehash: 519b60f63da38192e2196014e0ea7820dafd5491
ms.sourcegitcommit: 8a8c89b0ff6d6dfb8554b92187aca1bf0f8bcc07
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97618970"
---
# <a name="quickstart-connect-and-query-a-sql-server-instance-using-sql-server-management-studio-ssms"></a>Início Rápido: Conectar-se a uma instância do SQL Server e consultá-la usando o SSMS (SQL Server Management Studio)

[!INCLUDE [sqlserver](../../includes/applies-to-version/sqlserver.md)]

Introdução ao uso do SSMS (SQL Server Management Studio) para se conectar à instância do SQL Server e executar alguns comandos T-SQL (Transact-SQL).

O artigo demonstra como fazer o seguinte nas etapas abaixo:

> [!div class="checklist"]
> - Conectar a uma instância do SQL Server
> - Criar um banco de dados
> - Criar uma tabela no novo banco de dados
> - Inserir linhas na nova tabela
> - Consultar a nova tabela e exibir os resultados
> - Usar a tabela da janela de consulta para verificar as propriedades da conexão

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md) instalado.
- [Instância do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) instalada e configurada.

## <a name="connect-to-a-sql-server-instance"></a>Conectar a uma instância do SQL Server

1. Inicie o SQL Server Management Studio. Na primeira vez em que você executar o SSMS, a janela **Conectar-se ao Servidor** será aberta. Se ela não for aberta, você poderá abri-la manualmente selecionando **Pesquisador de Objetos** > **Conectar** > **Mecanismo de Banco de Dados**.

    :::image type="content" source="media/ssms-connect-query-sql-server/connect-object-explorer.png" alt-text="Link Conectar no Pesquisador de Objetos":::

2. A caixa de diálogo **Conectar-se ao Servidor** é exibida. Insira as seguintes informações:

    |   Configuração   |   Valores sugeridos   |   Descrição   |
    |--------------|-----------------------|-----------------|
    | **Tipo de servidor** | Mecanismo de banco de dados | Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados** (geralmente a opção padrão). |
    | **Nome do servidor** | O nome do servidor totalmente qualificado | Em **Nome do servidor**, insira o nome do SQL Server (você também poderá usar *localhost* como o nome do servidor se estiver se conectando localmente). Se NÃO estiver usando a instância padrão (***MSSQLSERVER** _), insira o nome do servidor e o nome da instância. </br> </br> Se você não tiver certeza de como determinar o nome da instância do SQL Server, confira [Mais dicas e truques para usar o SSMS](../tutorials/ssms-tricks.md#find-sql-server-instance-name). |
    | _ *Autenticação** | Autenticação do Windows </br> </br> Autenticação do SQL Server | A Autenticação do Windows é definida como padrão. </br> </br> Use também a **Autenticação do SQL Server** para se conectar. No entanto, se você selecionar **Autenticação do SQL Server**, um nome de usuário e uma senha serão necessários. </br> </br> Para obter mais informações sobre os tipos de autenticação, confira [Conectar ao servidor (mecanismo de banco de dados)](../f1-help/connect-to-server-database-engine.md). |
    | **Logon** | ID de usuário da conta do servidor | A ID de usuário da conta do servidor usada para fazer logon no servidor. Um logon é necessário ao usar a **Autenticação do SQL Server**. |
    | **Senha** | Senha da conta do servidor | A senha da conta do servidor usada para fazer logon no servidor. É necessário ter uma senha ao usar a **Autenticação do SQL Server**. |

    :::image type="content" source="media/ssms-connect-query-sql-server/connect-to-sql-server-object-explorer.png" alt-text="Campo de nome do servidor para o SQL Server":::

3. Depois de preencher todos os campos, selecione **Conectar**.

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todos os campos.

4. Para verificar se a conexão do SQL Server foi bem-sucedida, expanda e explore os objetos dentro do **Pesquisador de Objetos**, em que o nome do servidor, a versão do SQL Server e o nome de usuário são exibidos. Esses objetos são diferentes, dependendo do tipo de servidor.

    :::image type="content" source="media/ssms-connect-query-sql-server/connect-on-prem.png" alt-text="Conectando-se a um servidor local":::

## <a name="troubleshoot-connectivity-issues"></a>Solucionar problemas de conectividade

Para examinar as técnicas de solução de problemas a serem usadas quando não for possível se conectar a uma instância do Mecanismo de Banco de Dados do SQL Server em um só servidor, acesse [Solução de problemas de conexão ao Mecanismo de Banco de Dados do SQL Server](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="create-a-database"></a>Criar um banco de dados

Agora vamos criar um banco de dados chamado TutorialDB seguindo as etapas abaixo:

1. Clique com o botão direito do mouse na instância do servidor no Pesquisador de Objetos e selecione **Nova Consulta**:

   :::image type="content" source="media/ssms-connect-query-sql-server/new-query.png" alt-text="O link de nova consulta":::

2. Cole o seguinte snippet de código T-SQL na janela de consulta:

    ```sql
    USE master
    GO
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB]
    GO
   ```

3. Execute a consulta selecionando **Executar** ou F5 no teclado.

   :::image type="content" source="media/ssms-connect-query-sql-server/execute.png" alt-text="O comando Executar":::
  
    Depois que a consulta for concluída, o novo banco de dados TutorialDB aparecerá na lista de bancos de dados no Pesquisador de Objetos. Se ele não for exibido, clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Atualizar**.

## <a name="create-a-table-in-the-new-database"></a>Criar uma tabela no novo banco de dados

Nesta seção, você criará uma tabela no banco de dados TutorialDB recém-criado. Como o editor de consultas ainda está no contexto do banco de dados *mestre*, mude o contexto de conexão para o banco de dados *TutorialDB* executando as seguintes etapas:

1. Selecione o banco de dados desejado na lista suspensa de bancos de dados, conforme é mostrado aqui:

   :::image type="content" source="media/ssms-connect-query-sql-server/change-db.png" alt-text="Alterar banco de dados":::

2. Cole o seguinte snippet de código T-SQL na janela de consulta:

    ```sql
    USE [TutorialDB]
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

3. Execute a consulta selecionando **Executar** ou F5 no teclado.

Depois que a consulta for concluída, a nova tabela Clientes será exibida na lista de tabelas no Pesquisador de Objetos. Se a tabela não for exibida, clique com o botão direito do mouse no nó **TutorialDB** > **Tabelas** no Pesquisador de Objetos e selecione **Atualizar**.

   :::image type="content" source="media/ssms-connect-query-sql-server/new-table.png" alt-text="Nova tabela":::

## <a name="insert-rows-into-the-new-table"></a>Inserir linhas na nova tabela

Agora vamos inserir algumas linhas na tabela Customers criada. Cole o seguinte snippet de código T-SQL na janela de consulta e, em seguida, selecione **Executar**:

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

## <a name="query-the-table-and-view-the-results"></a>Consultar a tabela e exibir os resultados

Os resultados de uma consulta são exibidos abaixo da janela de texto de consulta. Para consultar a tabela Customers e ver as linhas que foram inseridas, siga as etapas abaixo:

1. Cole o seguinte snippet de código T-SQL na janela de consulta e, em seguida, selecione **Executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    Os resultados da consulta são exibidos na área em que o texto foi inserido.

   :::image type="content" source="media/ssms-connect-query-sql-server/query-results.png" alt-text="A lista de resultados":::

    Modifique também a maneira em que os resultados são apresentados selecionando uma das seguintes opções:

   ![Três opções para exibir os resultados da consulta](media/ssms-connect-query-sql-server/results.png)

   - O primeiro botão exibe os resultados na **Exibição de Texto**, conforme é mostrado na imagem na próxima seção.
   - O botão do meio exibe os resultados na **Exibição em Grade**, que é a opção padrão.
       - Isso é definido como padrão
   - O terceiro botão permite salvar os resultados em um arquivo cuja extensão é .rpt por padrão.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificar as propriedades da conexão usando a tabela da janela de consulta

Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. Depois de executar na etapa anterior a consulta já mencionada, examine as propriedades de conexão na parte inferior da janela de consulta.

- É possível determinar o servidor e o banco de dados aos quais você está conectado e o nome de usuário que você usa.
- Também é possível exibir a duração da consulta e o número de linhas retornadas pela consulta executada anteriormente.

   :::image type="content" source="media/ssms-connect-query-sql-server/connection-properties.png" alt-text="Propriedades da conexão":::

## <a name="additional-tools"></a>Ferramentas adicionais

Use também o [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para se conectar ao [SQL Server](../../azure-data-studio/quickstart-sql-server.md), a um [Banco de Dados SQL do Azure](../../azure-data-studio/quickstart-sql-database.md) e ao [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md) e consultá-los.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Esses artigos ajudam nos diversos recursos disponíveis no SSMS.

- [Editor de Consulta do SSMS (SQL Server Management Studio)](../f1-help/database-engine-query-editor-sql-server-management-studio.md)
- [Script](../tutorials/scripting-ssms.md)
- [Usando modelos no SSMS](../template/templates-ssms.md)
- [Configuração do SSMS](../tutorials/ssms-configuration.md)
- [Mais dicas e truques para usar o SSMS](../tutorials/ssms-tricks.md)