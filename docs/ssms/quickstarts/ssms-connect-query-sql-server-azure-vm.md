---
title: Conectar e consultar uma instância do SQL Server em uma VM do Azure usando o SSMS (SQL Server Management Studio)
description: Conecte-se a uma instância do SQL Server em uma VM do Azure usando o SSMS. Crie e consulte o SQL Server em uma VM do Azure executando consultas T-SQL básicas no SSMS.
ms.prod: sql
ms.technology: ssms
ms.topic: quickstart
author: markingmyname
ms.author: maghan
ms.reviewer: sstein, mikeray
ms.custom: contperf-fy21q2
ms.date: 12/15/2020
ms.openlocfilehash: 29c39caf6885ee974c62ed153df982b435c72c95
ms.sourcegitcommit: 8a8c89b0ff6d6dfb8554b92187aca1bf0f8bcc07
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97618989"
---
# <a name="quickstart-connect-and-query-a-sql-server-instance-on-an-azure-virtual-machine-using-sql-server-management-studio-ssms"></a>Início Rápido: Conectar-se a uma instância do SQL Server em uma máquina virtual do Azure e consultá-la usando o SSMS (SQL Server Management Studio)

[!INCLUDE [sqlserver](../../includes/applies-to-version/sqlserver.md)]

Introdução ao uso do SSMS (SQL Server Management Studio) para se conectar à instância do SQL Server em uma Máquina Virtual do Azure e executar alguns comandos T-SQL (Transact-SQL).

> [!div class="checklist"]
> - Conectar a uma instância do SQL Server
> - Criar um banco de dados
> - Criar uma tabela no novo banco de dados
> - Inserir linhas na nova tabela
> - Consultar a nova tabela e exibir os resultados
> - Usar a tabela da janela de consulta para verificar as propriedades da conexão
## <a name="prerequisites"></a>Pré-requisitos

Para concluir este artigo, você precisará do SQL Server Management Studio e ter acesso a uma fonte de dados.

- Instale o [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md).
- [SQL Server em uma VM do Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/?&ef_id=CjwKCAiA17P9BRB2EiwAMvwNyP3g3mY45X8dbqEtIr8HASwSLUYRBrwwciZptYt0vUU4K7TuWnXTbxoCoPQQAvD_BwE:G:s&OCID=AID2100131_SEM_CjwKCAiA17P9BRB2EiwAMvwNyP3g3mY45X8dbqEtIr8HASwSLUYRBrwwciZptYt0vUU4K7TuWnXTbxoCoPQQAvD_BwE:G:s&gclid=CjwKCAiA17P9BRB2EiwAMvwNyP3g3mY45X8dbqEtIr8HASwSLUYRBrwwciZptYt0vUU4K7TuWnXTbxoCoPQQAvD_BwE).

## <a name="connect-to-sql-virtual-machines"></a>Conectar-se às Máquinas Virtuais do SQL

As etapas a seguir mostram como criar um rótulo DNS opcional para sua VM do Azure e, em seguida, conectar-se com o SSMS (SQL Server Management Studio).

### <a name="configure-a-dns-label-for-the-public-ip-address"></a>Configurar um rótulo de DNS para o endereço IP público

Para conectar o Mecanismo de Banco de Dados do SQL Server na Internet, considere criar um Rótulo DNS para seu endereço IP público. Você pode se conectar pelo endereço IP, mas o rótulo DNS cria um Registro A que é mais fácil de ser identificado e elimina o endereço IP público subjacente.

> [!NOTE]
> Rótulos de DNS não são obrigatórios se você planeja se conectar somente à instância do SQL Server na mesma Rede Virtual ou apenas localmente.

1. Crie um rótulo DNS selecionando **Máquinas virtuais** no portal. Selecione sua VM do SQL Server para exibir suas propriedades.

2. Na visão geral da máquina virtual, selecione seu **Endereço IP público**.

    :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/azure-sql-vm-ip-address-.png" alt-text="endereço IP público":::

3. Nas propriedades de seu Endereço IP Público, expanda **Configuração**.

4. Insira um nome para o rótulo de DNS. Esse nome é um Registro A que pode ser usado para se conectar diretamente à VM do SQL Server por nome em vez de por endereço IP.

5. Selecione o botão **Salvar**.

    :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/azure-sql-vm-dns-label.png" alt-text="rótulo DNS":::

### <a name="connect"></a>Conectar

1. Inicie o SQL Server Management Studio. Na primeira vez em que você executar o SSMS, a janela **Conectar-se ao Servidor** será aberta. Se ela não for aberta, você poderá abri-la manualmente selecionando **Pesquisador de Objetos** > **Conectar** > **Mecanismo de Banco de Dados**.

    :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/connect-object-explorer.png" alt-text="Link Conectar no Pesquisador de Objetos":::

2. A caixa de diálogo **Conectar-se ao Servidor** é exibida. Insira as seguintes informações:

    |   Configuração   |   Valores sugeridos   |   Descrição   |
    |--------------|-----------------------|-----------------|
    | **Tipo de servidor** | Mecanismo de banco de dados | Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados** (geralmente a opção padrão). |
    | **Nome do servidor** | O nome do servidor totalmente qualificado | Em **Nome do servidor**, insira o nome da VM do SQL do Azure. Use também o endereço IP da VM do SQL do Azure para se conectar. | 
    | **Autenticação** | Autenticação do SQL Server | Use a **Autenticação do SQL Server** para a VM do SQL do Azure para se conectar. Além disso, se você tiver uma configuração de ambiente do Azure Active Directory, use uma das opções do Azure Active Directory. </br> </br> Não há suporte para o método de **Autenticação do Windows** na VM do SQL do Azure. Para obter mais informações, confira [Autenticação do SQL do Azure](/azure/sql-database/sql-database-security-overview#access-management).|
    | **Logon** | ID de usuário da conta do servidor | A ID de usuário da conta do servidor usada para criar o servidor. Um logon é necessário ao usar a **Autenticação do SQL Server**. |
    | **Senha** | Senha da conta do servidor | A senha da conta do servidor usada para criar o servidor. É necessário ter uma senha ao usar a **Autenticação do SQL Server**. |

    :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/connect-to-azure-sql-vm-object-explorer.png" alt-text="Campo de nome do servidor para máquinas virtuais do SQL":::

3. Depois de preencher todos os campos, selecione **Conectar**.

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todas as opções.

4. Para verificar se o SQL Server na VM do Azure foi bem-sucedida, expanda e explore os objetos dentro do **Pesquisador de Objetos**, em que o nome do servidor, a versão do SQL Server e o nome de usuário são exibidos. Esses objetos são diferentes, dependendo do tipo de servidor.

    :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/connect-azure-sql-vm.png" alt-text="conexão de VM do SQL do Azure":::

## <a name="troubleshoot-connectivity-issues"></a>Solucionar problemas de conectividade

Embora o portal forneça opções para configurar a conectividade automaticamente, é bom saber como configurar a conectividade manualmente. Entender os requisitos também pode ajudar a solucionar problemas.

A tabela a seguir lista os requisitos para se conectar ao SQL Server na VM do Azure.

| Requisito | Descrição |
|---|---|
| [Habilitar o modo de autenticação do SQL Server](/sql/database-engine/configure-windows/change-server-authentication-mode#use-ssms) | A autenticação do SQL Server é necessária para conectar-se remotamente à VM, a menos que o Active Directory esteja configurado em uma rede virtual. |
| [Criar um logon do SQL](/sql/relational-databases/security/authentication-access/create-a-login) | Se você estiver usando a autenticação do SQL, precisará de um logon do SQL com um nome de usuário e uma senha que também tenha permissões para o banco de dados de destino. |
| Habilitar o protocolo TCP/IP | O SQL Server deve permitir conexões por meio de TCP. |
| [Habilitar a regra de firewall para a porta do SQL Server](/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access) | O firewall na VM deve permitir tráfego de entrada na porta do SQL Server (padrão 1433). |
| [Criar uma regra do grupo de segurança de rede para TCP 1433](https://docs.microsoft.com/azure/virtual-network/manage-network-security-group#create-a-security-rule) | Permita que a VM receba o tráfego na porta do SQL Server (padrão 1433) se desejar se conectar à Internet. Isso não é necessário para conexões somente de rede local e virtual. Esta etapa só é necessária no portal do Azure. |

> [!TIP]
> As etapas na tabela acima serão executadas automaticamente quando você configurar a conectividade no portal. Use essas etapas apenas para confirmar sua configuração ou ao configurar manualmente a conectividade do SQL Server.

## <a name="create-a-database"></a>Criar um banco de dados

Crie um banco de dados chamado TutorialDB seguindo estas etapas:

1. Clique com o botão direito do mouse na instância do servidor no Pesquisador de Objetos e selecione **Nova Consulta**:

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/new-query.png" alt-text="O link de nova consulta":::

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

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/execute.png" alt-text="O comando Executar":::
  
    Depois que a consulta for concluída, o novo banco de dados TutorialDB aparecerá na lista de bancos de dados no Pesquisador de Objetos. Se ele não for exibido, clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Atualizar**.

## <a name="create-a-table-in-the-new-database"></a>Criar uma tabela no novo banco de dados

Nesta seção, você criará uma tabela no banco de dados TutorialDB recém-criado. Como o editor de consultas ainda está no contexto do banco de dados *mestre*, mude o contexto de conexão para o banco de dados *TutorialDB* executando as seguintes etapas:

1. Selecione o banco de dados desejado na lista suspensa de bancos de dados, conforme é mostrado aqui:

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/change-db.png" alt-text="Alterar banco de dados":::

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

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/new-table.png" alt-text="Nova tabela":::

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

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/query-results.png" alt-text="A lista de resultados":::

    Modifique também a maneira em que os resultados são apresentados selecionando uma das seguintes opções:

   ![Três opções para exibir os resultados da consulta](media/ssms-connect-query-sql-server-azure-vm/results.png)

   - O primeiro botão exibe os resultados na **Exibição de Texto**, conforme é mostrado na imagem na próxima seção.
   - O botão do meio exibe os resultados na **Exibição em Grade**, que é a opção padrão.
       - Isso é definido como padrão
   - O terceiro botão permite salvar os resultados em um arquivo cuja extensão é .rpt por padrão.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificar as propriedades da conexão usando a tabela da janela de consulta

Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. Depois de executar na etapa anterior a consulta já mencionada, examine as propriedades de conexão na parte inferior da janela de consulta.

- É possível determinar o servidor e o banco de dados aos quais você está conectado e o nome de usuário que você usa.
- Também é possível exibir a duração da consulta e o número de linhas retornadas pela consulta executada anteriormente.

   :::image type="content" source="media/ssms-connect-query-sql-server-azure-vm/connection-properties.png" alt-text="Propriedades da conexão":::

## <a name="additional-tools"></a>Ferramentas adicionais

Use também o [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para se conectar ao [SQL Server](../../azure-data-studio/quickstart-sql-server.md), a um [Banco de Dados SQL do Azure](../../azure-data-studio/quickstart-sql-database.md) e ao [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md) e consultá-los.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Esses artigos ajudam nos diversos recursos disponíveis no SSMS.

- [Editor de Consulta do SSMS (SQL Server Management Studio)](../f1-help/database-engine-query-editor-sql-server-management-studio.md)
- [Script](../tutorials/scripting-ssms.md)
- [Usando modelos no SSMS](../template/templates-ssms.md)
- [Configuração do SSMS](../tutorials/ssms-configuration.md)
- [Mais dicas e truques para usar o SSMS](../tutorials/ssms-tricks.md)