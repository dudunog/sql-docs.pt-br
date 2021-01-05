---
title: Criar snippets de código reutilizáveis
description: Saiba como criar e usar snippets de código SQL do Azure Data Studio, que facilitam a criação de bancos de dados e objetos de banco de dados.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: bd86afbe288be3b92b15b6702ec46903f56a2ad5
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97637799"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-azure-data-studio"></a>Criar e usar snippets de código para criar scripts T-SQL (Transact-SQL) rapidamente no Azure Data Studio

Os snippets de código no Azure Data Studio são modelos que facilitam a criação de bancos de dados e objetos de banco de dados. 

O Azure Data Studio fornece vários snippets T-SQL para ajudar você a gerar rapidamente a sintaxe correta. 

Snippets de código definidos pelo usuário também podem ser criados.

## <a name="using-built-in-t-sql-code-snippets"></a>Como usar snippets de código T-SQL internos

1. Para acessar os snippets disponíveis, digite *sql* no editor de consultas para abrir a lista:

   ![snippets](media/code-snippets/sql-snippets.png)

2. Selecione o snippet que deseja usar e ele gerará o script T-SQL. Por exemplo, selecione *sqlCreateTable*:

   ![snippets de create table](media/code-snippets/create-table.png)

3. Atualize os campos realçados com seus valores específicos. Por exemplo, substitua *TableName* e *Schema* pelos valores do banco de dados:

   ![Tabela do snippet](media/code-snippets/table-from-snippet.png)

   Se o campo que você deseja alterar não estiver mais realçado (isso acontece ao mover o cursor em torno do editor), clique com o botão direito do mouse na palavra que deseja alterar e selecione **Alterar todas as ocorrências**:

   ![Alterar tudo](media/code-snippets/change-all.png)

4. Atualize ou adicione qualquer T-SQL adicional necessário para o snippet selecionado. Por exemplo, atualize *Column1*, *Column2* e adicione mais colunas.

## <a name="creating-sql-code-snippets"></a>Como criar snippets de código SQL

Você pode definir seus próprios snippets. Para abrir o arquivo de snippet SQL para edição:

1. Abra a *paleta de comandos* (**Shift+Ctrl+P**), digite *captura* e selecione **Preferências: Abrir Snippets de Usuário**:

   ![Snippets de usuário](media/code-snippets/user-snippets.png)

2. Selecione **SQL**:

   > [!NOTE]
   > O Azure Data Studio herda a funcionalidade de snippet de código do Visual Studio Code e, portanto, este artigo aborda especificamente o uso de snippets SQL. Para obter informações mais detalhadas, confira [Como criar seus próprios snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) na documentação do Visual Studio Code. 

   ![Selecionar SQL](media/code-snippets/select-sql.png)

3. Cole o seguinte código em *sql.json*:

    ```sql
    {
     "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "$1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "Column1 [NVARCHAR](50) NOT NULL,",
    "Column2 [NVARCHAR](50) NOT NULL",
    "-- specify more columns here",
    ");",
    "GO"
    ],
       "description": "User-defined snippet example 2"
       }
       }
    ```

4. Salve o arquivo sql.json.

5. Abra uma nova janela do editor de consultas clicando em **Ctrl+N**.

6. Digite **sql** e você verá os dois snippets de usuário recém-adicionados: *sqlCreateTable2* e *sqlSelectTop5*.

Selecione um dos novos snippets e experimente uma execução de teste.

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre o editor SQL, confira [Tutorial do editor de códigos](tutorial-sql-editor.md).
