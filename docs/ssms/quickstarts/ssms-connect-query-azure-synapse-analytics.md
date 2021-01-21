---
title: Conectar e consultar um pool de SQL dedicado no Azure Synapse Analytics com o SSMS (SQL Server Management Studio)
description: Conecte-se a um pool de SQL dedicado no Azure Synapse Analytics usando o SSMS. Crie e consulte um pool de SQL dedicado no Azure Synapse Analytics executando consultas T-SQL básicas no SSMS.
ms.prod: sql
ms.technology: ssms
ms.topic: quickstart
author: markingmyname
ms.author: maghan
ms.reviewer: sstein, mikeray
ms.custom: contperf-fy21q2
ms.date: 12/15/2020
ms.openlocfilehash: e3584fe72ada1cff1d3b35324c5c5563bf97d050
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596849"
---
# <a name="quickstart-connect-and-query-a-dedicated-sql-pool-in-azure-synapse-analytics-with-sql-server-management-studio-ssms"></a>Início Rápido: Conectar e consultar um pool de SQL dedicado no Azure Synapse Analytics com o SSMS (SQL Server Management Studio)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Introdução ao uso do SSMS (SQL Server Management Studio) para se conectar ao pool de SQL dedicado no Azure Synapse Analytics e executar alguns comandos T-SQL (Transact-SQL).

> [!div class="checklist"]
> - Conectar-se a um pool de SQL dedicado no Azure Synapse Analytics
> - Criar um banco de dados
> - Criar uma tabela no novo banco de dados
> - Inserir linhas na nova tabela
> - Consultar a nova tabela e exibir os resultados
> - Usar a tabela da janela de consulta para verificar as propriedades da conexão

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este artigo, você precisará do SQL Server Management Studio e ter acesso a uma fonte de dados.

- Instale o [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md).
- [Azure Synapse Analytics](https://azure.microsoft.com/services/synapse-analytics/?&ef_id=CjwKCAiA17P9BRB2EiwAMvwNyDW39uBCUDMPmL693_KrmcNAV2uiMHZDeNJ-615AoxdIPBNqXwBDMhoCkL8QAvD_BwE:G:s&OCID=AID2100131_SEM_CjwKCAiA17P9BRB2EiwAMvwNyDW39uBCUDMPmL693_KrmcNAV2uiMHZDeNJ-615AoxdIPBNqXwBDMhoCkL8QAvD_BwE:G:s&gclid=CjwKCAiA17P9BRB2EiwAMvwNyDW39uBCUDMPmL693_KrmcNAV2uiMHZDeNJ-615AoxdIPBNqXwBDMhoCkL8QAvD_BwE)

## <a name="connect-to-a-dedicated-sql-pool-in-azure-synapse-analytics"></a>Conectar-se a um pool de SQL dedicado no Azure Synapse Analytics

[!INCLUDE[ssms-connect-azure-ad](../../includes/ssms-connect-azure-ad.md)]

1. Inicie o SQL Server Management Studio. Na primeira vez em que você executar o SSMS, a janela **Conectar-se ao Servidor** será aberta. Se ela não for aberta, você poderá abri-la manualmente selecionando **Pesquisador de Objetos** > **Conectar** > **Mecanismo de Banco de Dados**.

    :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/connect-object-explorer.png" alt-text="Link Conectar no Pesquisador de Objetos":::

2. Na janela **Conectar-se ao servidor**, siga a lista a seguir:

    |   Setting   |   Valores sugeridos   |   Descrição   |
    |-------------|------------------------|-----------------|
    | **Tipo de servidor** | Mecanismo de banco de dados | Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados** (geralmente a opção padrão). |
    | **Nome do servidor** | O nome do servidor totalmente qualificado | Em **Nome do servidor**, insira o nome do servidor do Azure Synapse Analytics. |
    | **Autenticação** | Autenticação do SQL Server | Use a **Autenticação do SQL Server** para o Azure Synapse Analytics para se conectar. </br> </br> Não há suporte para o método de **Autenticação do Windows** no SQL do Azure. Para obter mais informações, confira [Autenticação do SQL do Azure](/azure/sql-database/sql-database-security-overview#access-management). |
    | **Logon** | ID de usuário da conta do servidor | A ID de usuário da conta do servidor usada para criar o servidor. |
    | **Senha** | Senha da conta do servidor | A senha da conta do servidor usada para criar o servidor. |

    :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/connect-to-azure-synapse-analytics-object-explorer.png" alt-text="Campo de nome do servidor para o Azure Synapse Analytics":::

3. Depois de preencher todos os campos, selecione **Conectar**.

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todas as opções.

    Se você ainda não definiu as configurações do firewall, um aviso é exibido para configurá-lo. Depois de se conectar, preencha suas informações de logon da conta do Azure e prossiga para definir a regra de firewall. Depois, selecione **OK**. Essa solicitação é uma ação que será realizada uma vez. Depois que você configurar o firewall, o aviso de firewall não será exibido.

    :::image type="content" source="media/ssms-connect-query-azure-sql/azure-sql-firewall-sign-in-3.png" alt-text="Nova regra de firewall do SQL do Azure":::

4. Para verificar se a conexão do Azure Synapse Analytics foi bem-sucedida, expanda e explore os objetos dentro do **Pesquisador de Objetos**, em que o nome do servidor, a versão do SQL Server e o nome de usuário são exibidos. Esses objetos são diferentes, dependendo do tipo de servidor.

    :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/connect-azure-synapse-analytics.png" alt-text="Como se conectar a um banco de dados do Azure Synapse Analytics":::

## <a name="troubleshoot-connectivity-issues"></a>Solucionar problemas de conectividade

Você pode enfrentar problemas de conexão com o Azure Synapse Analytics. Para obter mais informações sobre como solucionar problemas de conexão, acesse [Solução de problemas de conectividade](/azure/azure-sql/database/troubleshoot-common-errors-issues).

Você pode evitar, solucionar, diagnosticar e atenuar erros transitórios e de conexão encontrados ao interagir com o Banco de Dados SQL do Azure ou a Instância Gerenciada de SQL do Azure. Para obter mais informações, acesse [Solução de erros de conexão transitória](/azure/azure-sql/database/troubleshoot-common-connectivity-issues).

## <a name="create-a-database"></a>Criar um banco de dados

Agora vamos criar um banco de dados chamado TutorialDB seguindo as etapas abaixo:

1. Clique com o botão direito do mouse na instância do servidor no Pesquisador de Objetos e selecione **Nova Consulta**:

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/new-query.png" alt-text="O link de nova consulta":::

2. Cole o seguinte snippet de código T-SQL na janela de consulta:

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

3. Execute a consulta selecionando **Executar** ou F5 no teclado.

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/execute.png" alt-text="O comando Executar":::
  
    Depois que a consulta for concluída, o novo banco de dados TutorialDB aparecerá na lista de bancos de dados no Pesquisador de Objetos. Se ele não for exibido, clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Atualizar**.

## <a name="create-a-table-in-the-new-database"></a>Criar uma tabela no novo banco de dados

Nesta seção, você criará uma tabela no banco de dados TutorialDB recém-criado. Como o editor de consultas ainda está no contexto do banco de dados *mestre*, mude o contexto de conexão para o banco de dados *TutorialDB* executando as seguintes etapas:

1. Selecione o banco de dados desejado na lista suspensa de bancos de dados, conforme é mostrado aqui:

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/change-db.png" alt-text="Alterar banco de dados":::

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

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/new-table.png" alt-text="Nova tabela":::

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

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/query-results.png" alt-text="A lista de resultados":::

    Modifique também a maneira em que os resultados são apresentados selecionando uma das seguintes opções:

   ![Três opções para exibir os resultados da consulta](media/ssms-connect-query-azure-synapse-analytics/results.png)

   - O primeiro botão exibe os resultados na **Exibição de Texto**, conforme é mostrado na imagem na próxima seção.
   - O botão do meio exibe os resultados na **Exibição em Grade**, que é a opção padrão.
       - Isso é definido como padrão
   - O terceiro botão permite salvar os resultados em um arquivo cuja extensão é .rpt por padrão.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificar as propriedades da conexão usando a tabela da janela de consulta

Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. Depois de executar na etapa anterior a consulta já mencionada, examine as propriedades de conexão na parte inferior da janela de consulta.

- É possível determinar o servidor e o banco de dados aos quais você está conectado e o nome de usuário que você usa.
- Também é possível exibir a duração da consulta e o número de linhas retornadas pela consulta executada anteriormente.

   :::image type="content" source="media/ssms-connect-query-azure-synapse-analytics/connection-properties.png" alt-text="Propriedades da conexão":::

## <a name="additional-tools"></a>Ferramentas adicionais

Use também o [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para se conectar ao [SQL Server](../../azure-data-studio/quickstart-sql-server.md), a um [Banco de Dados SQL do Azure](../../azure-data-studio/quickstart-sql-database.md) e ao [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md) e consultá-los.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Esses artigos ajudam nos diversos recursos disponíveis no SSMS.

- [Editor de Consulta do SSMS (SQL Server Management Studio)](../f1-help/database-engine-query-editor-sql-server-management-studio.md)
- [Script](../tutorials/scripting-ssms.md)
- [Usando modelos no SSMS](../template/templates-ssms.md)
- [Configuração do SSMS](../tutorials/ssms-configuration.md)
- [Mais dicas e truques para usar o SSMS](../tutorials/ssms-tricks.md)