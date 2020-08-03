---
title: 'Início Rápido: Conectar-se ao PostgreSQL e consultá-lo'
description: Faça um início rápido no qual você usa o Azure Data Studio para conectar-se ao PostgreSQL e usa instruções SQL para criar e consultar um banco de dados.
ms.custom: seodec18
ms.date: 09/18/2019
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: e2ba0f0123faeacd0f431a72ef35add40ee48e19
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411302"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-postgresql"></a>Início Rápido: Usar o Azure Data Studio para conectar-se ao PostgreSQL e consultá-lo

Este guia de início rápido mostra como usar o Azure Data Studio para conectar-se ao PostgreSQL e usar instruções SQL para criar o banco de dados *tutorialdb* e consultá-lo.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este guia de início rápido, você precisa do Azure Data Studio, da extensão PostgreSQL para Azure Data Studio e acesso a um servidor PostgreSQL.

- [Instale o Azure Data Studio](download.md).
- [Instalar extensão do PostgreSQL para o Azure Data Studio](postgres-extension.md).
- [Instalar o PostgreSQL](https://www.postgresql.org/download/). (Como alternativa, você pode criar um banco de dados Postgres na nuvem usando [az postgres up](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Conectar-se ao PostgreSQL

1. Inicie o **Azure Data Studio**.

2. Na primeira vez que você iniciar o Azure Data Studio, a caixa de diálogo **Conexão** será aberta. Se a caixa de diálogo **Conexão** não abrir, clique no ícone **Nova Conexão** na página **SERVIDORES**:

   ![Ícone de Nova Conexão](media/quickstart-postgresql/new-connection-icon.png)

3. No formulário que aparece, vá para **Tipo de conexão** e selecione **PostgreSQL** na lista suspensa.


4. Preencha os campos restantes usando o nome do servidor, o nome de usuário e a senha para o servidor PostgreSQL. 

   ![Nova Tela de Conexão](media/quickstart-postgresql/new-connection-screen.png)  

   | Configuração       | Valor de exemplo | Descrição |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | localhost | O nome do servidor totalmente qualificado |
   | **Nome de usuário** | postgres | O nome de usuário com o qual você deseja fazer logon. |
   | **Senha (Logon do SQL)** | *password* | A senha da conta com a qual você está fazendo logon. |
   | **Senha** | *Verificação* | Marque esta caixa se não quiser inserir a senha toda vez que se conectar. |
   | **Nome do banco de dados** | \<Default\> | Preencha isto se você quiser que a conexão especifique um banco de dados. |
   | **Grupo de servidor** | \<Default\> | Essa opção permite atribuir essa conexão a um grupo de servidores específico que você cria. | 
   | **Nome (opcional)** | *deixar em branco* | Esta opção permite especificar um nome amigável para o servidor. | 

5. Selecione **Conectar**. 

Depois de se conectar com êxito, o servidor será aberto na barra lateral **SERVIDORES**.


## <a name="create-a-database"></a>Criar um banco de dados

As etapas a seguir criam outro banco de dados denominado **tutorialdb**:

1. Clique com o botão direito do mouse no servidor PostgreSQL na barra lateral **SERVIDORES** e selecione **Nova Consulta**.

2. Cole essa instrução SQL no editor de consultas que é aberto.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. Na barra de ferramentas, selecione **Executar** para executar a consulta. As notificações aparecem no painel **MENSAGENS** para mostrar o progresso da consulta.

>[!TIP]
> Você pode usar **F5** no teclado para executar a instrução, em vez de usar **Executar**.

Após a conclusão da consulta, clique com o botão direito do mouse em **Bancos de dados** e selecione **Atualizar** para ver **tutorialdb** na lista sob o nó **Bancos de Dados**.


## <a name="create-a-table"></a>Criar uma tabela

 As etapas a seguir criam uma tabela no **tutorialdb**:

1. Altere o contexto de conexão para **tutorialdb** usando a lista suspensa no editor de consultas. 

   ![Alterar contexto](media/quickstart-postgresql/change-context.png)

2. Cole o snippet a seguinte instrução SQL no editor de consultas e clique em **Executar**. 

   > [!NOTE]
   > Você pode acrescentar isto ou substituir a consulta existente no editor. Clicar em **Executar** executa apenas a consulta realçada. Se nada estiver realçado, clicar em **Executar** executará todas as consultas no editor.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Inserir linhas

Cole o snippet a seguir na janela de consultas e clique em **Executar**:

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Consultar os dados

1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Os resultados da consulta são exibidos:

   ![Exibir os resultados](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os [cenários disponíveis para Postgres no Azure Data Studio](postgres-extension.md). 