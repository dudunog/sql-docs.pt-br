---
title: Conectar-se a um Banco de Dados SQL do Azure ou uma Instância Gerenciada do Azure e consultá-los usando o SSMS (SQL Server Management Studio)
description: Conecte-se a um Banco de Dados SQL do Azure ou a uma Instância Gerenciada do Azure no SSMS. Crie e consulte um Banco de Dados SQL do Azure ou uma Instância Gerenciada do Azure no SSMS executando consultas T-SQL básicas.
ms.prod: sql
ms.technology: ssms
ms.topic: quickstart
author: markingmyname
ms.author: maghan
ms.reviewer: sstein, mikeray
ms.custom: contperf-fy21q2
ms.date: 12/15/2020
ms.openlocfilehash: bb1eeea5d336ccba441cea5c6089d326c33dbdaf
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98597338"
---
# <a name="quickstart-connect-and-query-an-azure-sql-database-or-an-azure-managed-instance-using-sql-server-management-studio-ssms"></a>Início Rápido: Conectar-se a um Banco de Dados SQL do Azure ou uma Instância Gerenciada do Azure e consultá-los usando o SSMS (SQL Server Management Studio)

[!INCLUDE [asdb](../../includes/applies-to-version/asdb.md)]

Introdução ao uso do SSMS (SQL Server Management Studio) para se conectar ao Banco de Dados SQL do Azure e executar alguns comandos T-SQL (Transact-SQL).

O artigo demonstra como fazer o seguinte nas etapas abaixo:

> [!div class="checklist"]
> - Conectar-se a um banco de dados SQL do Azure
> - Criar um banco de dados
> - Criar uma tabela no novo banco de dados
> - Inserir linhas na nova tabela
> - Consultar a nova tabela e exibir os resultados
> - Usar a tabela da janela de consulta para verificar as propriedades da conexão

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md) instalado.
- [Banco de Dados SQL do Azure](https://azure.microsoft.com/free/sql-database/search/?&ef_id=CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE:G:s&OCID=AID2100131_SEM_CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE:G:s&gclid=CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE) ou [Instância Gerenciada de SQL do Azure](https://azure.microsoft.com/services/azure-sql/sql-managed-instance/)

## <a name="connect-to-an-azure-sql-database-or-azure-sql-managed-instance"></a>Conectar-se a um Banco de Dados SQL do Azure ou a uma Instância Gerenciada de SQL do Azure

[!INCLUDE[ssms-connect-azure-ad](../../includes/ssms-connect-azure-ad.md)]

1. Inicie o SQL Server Management Studio. Na primeira vez em que você executar o SSMS, a janela **Conectar-se ao Servidor** será aberta. Se ela não for aberta, você poderá abri-la manualmente selecionando **Pesquisador de Objetos** > **Conectar** > **Mecanismo de Banco de Dados**.

    :::image type="content" source="media/ssms-connect-query-azure-sql/connect-object-explorer.png" alt-text="Link Conectar no Pesquisador de Objetos":::

2. A caixa de diálogo **Conectar-se ao Servidor** é exibida. Insira as seguintes informações:

    |   Configuração   |   Valores sugeridos   |   Descrição   |
    |-------------|------------------------|-----------------|
    | **Tipo de servidor** | Mecanismo de banco de dados | Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados** (geralmente a opção padrão). |
    | **Nome do servidor** | O nome do servidor totalmente qualificado | Em **Nome do servidor**, insira o nome do *Banco de Dados SQL do Azure* ou da *Instância Gerenciada do Azure*. |
    | **Autenticação** | Autenticação do SQL Server | Use a **Autenticação do SQL Server** para o SQL do Azure para se conectar. </br> </br> Não há suporte para o método de **Autenticação do Windows** no SQL do Azure. Para obter mais informações, confira [Autenticação do SQL do Azure](/azure/sql-database/sql-database-security-overview#access-management). |
    | **Logon** | ID de usuário da conta do servidor | A ID de usuário da conta do servidor usada para criar o servidor. |
    | **Senha** | Senha da conta do servidor | A senha da conta do servidor usada para criar o servidor. |

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todas as opções.

    :::image type="content" source="media/ssms-connect-query-azure-sql/connect-to-azure-sql-object-explorer.png" alt-text="Campo de nome do servidor para o SQL do Azure":::

3. Depois de preencher todos os campos, selecione **Conectar**.

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todas as opções.

   Se você ainda não definiu as configurações do firewall, um aviso é exibido para configurá-lo. Depois de se conectar, preencha suas informações de logon da conta do Azure e prossiga para definir a regra de firewall. Depois, selecione **OK**. Essa solicitação é uma ação que será realizada uma vez. Depois que você configurar o firewall, o aviso de firewall não será exibido.

    :::image type="content" source="media/ssms-connect-query-azure-sql/azure-sql-firewall-sign-in-3.png" alt-text="Nova regra de firewall do SQL do Azure":::

4. Para verificar se a conexão do Banco de Dados SQL do Azure ou da Instância Gerenciada do Azure foi bem-sucedida, expanda e explore os objetos no **Pesquisador de Objetos**, em que o nome do servidor, a versão do SQL Server e o nome de usuário são exibidos. Esses objetos são diferentes, dependendo do tipo de servidor.

    :::image type="content" source="media/ssms-connect-query-azure-sql/connect-azure-sql.png" alt-text="Conectando-se a um banco de dados SQL do Azure":::

## <a name="troubleshoot-connectivity-issues"></a>Solucionar problemas de conectividade

Você pode enfrentar problemas de conexão com o Azure Synapse Analytics. Para obter mais informações sobre como solucionar problemas de conexão, acesse [Solução de problemas de conectividade](/azure/azure-sql/database/troubleshoot-common-errors-issues).

Você pode evitar, solucionar, diagnosticar e atenuar erros transitórios e de conexão encontrados ao interagir com o Banco de Dados SQL do Azure ou a Instância Gerenciada de SQL do Azure. Para obter mais informações, acesse [Solução de erros de conexão transitória](/azure/azure-sql/database/troubleshoot-common-connectivity-issues).

## <a name="create-a-database"></a>Criar um banco de dados

Agora vamos criar um banco de dados chamado TutorialDB seguindo as etapas abaixo:

1. Clique com o botão direito do mouse na instância do servidor no Pesquisador de Objetos e selecione **Nova Consulta**:

   :::image type="content" source="media/ssms-connect-query-azure-sql/new-query.png" alt-text="O link de nova consulta":::

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

   :::image type="content" source="media/ssms-connect-query-azure-sql/execute.png" alt-text="O comando Executar":::
  
    Depois que a consulta for concluída, o novo banco de dados TutorialDB aparecerá na lista de bancos de dados no Pesquisador de Objetos. Se ele não for exibido, clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Atualizar**.

## <a name="create-a-table-in-the-new-database"></a>Criar uma tabela no novo banco de dados

Nesta seção, você criará uma tabela no banco de dados TutorialDB recém-criado. Como o editor de consultas ainda está no contexto do banco de dados *mestre*, mude o contexto de conexão para o banco de dados *TutorialDB* executando as seguintes etapas:

1. Selecione o banco de dados desejado na lista suspensa de bancos de dados, conforme é mostrado aqui:

   :::image type="content" source="media/ssms-connect-query-azure-sql/change-db.png" alt-text="Alterar banco de dados":::

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

   :::image type="content" source="media/ssms-connect-query-azure-sql/new-table.png" alt-text="Nova tabela":::

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

   :::image type="content" source="media/ssms-connect-query-azure-sql/query-results.png" alt-text="A lista de resultados":::

    Modifique também a maneira em que os resultados são apresentados selecionando uma das seguintes opções:

   ![Três opções para exibir os resultados da consulta](media/ssms-connect-query-azure-sql/results.png)

   - O primeiro botão exibe os resultados na **Exibição de Texto**, conforme é mostrado na imagem na próxima seção.
   - O botão do meio exibe os resultados na **Exibição em Grade**, que é a opção padrão.
       - Isso é definido como padrão
   - O terceiro botão permite salvar os resultados em um arquivo cuja extensão é .rpt por padrão.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificar as propriedades da conexão usando a tabela da janela de consulta

Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. Depois de executar na etapa anterior a consulta já mencionada, examine as propriedades de conexão na parte inferior da janela de consulta.

- É possível determinar o servidor e o banco de dados aos quais você está conectado e o nome de usuário que você usa.
- Também é possível exibir a duração da consulta e o número de linhas retornadas pela consulta executada anteriormente.

   :::image type="content" source="media/ssms-connect-query-azure-sql/connection-properties.png" alt-text="Propriedades da conexão":::

## <a name="additional-tools"></a>Ferramentas adicionais

Use também o [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para se conectar ao [SQL Server](../../azure-data-studio/quickstart-sql-server.md), a um [Banco de Dados SQL do Azure](../../azure-data-studio/quickstart-sql-database.md) e ao [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md) e consultá-los.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Esses artigos ajudam nos diversos recursos disponíveis no SSMS.

- [Editor de Consulta do SSMS (SQL Server Management Studio)](../f1-help/database-engine-query-editor-sql-server-management-studio.md)
- [Script](../tutorials/scripting-ssms.md)
- [Usando modelos no SSMS](../template/templates-ssms.md)
- [Configuração do SSMS](../tutorials/ssms-configuration.md)
- [Mais dicas e truques para usar o SSMS](../tutorials/ssms-tricks.md)