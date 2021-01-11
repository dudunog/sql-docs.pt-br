---
description: MSSQLSERVER_18483
title: MSSQLSERVER_18483
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18483 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 40a75d8ad0bd6237b594f38bbb5cb83be8cca788
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797817"
---
# <a name="mssqlserver_18483"></a>MSSQLSERVER_18483
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|18483|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|REMLOGIN_INVALID_USER|
|Texto da mensagem|Impossível estabelecer conexão com o servidor '%.ls' porque '%. ls' não está definido como logon remoto no servidor. Verifique se especificou o nome de logon correto. %.*ls.|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando você tenta configurar um distribuidor de replicação em um sistema que foi restaurado usando a imagem de disco rígido de outro computador em que a instância SQL foi originalmente instalada. Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> O SQL Server Management Studio não pôde configurar '\<Server>\<Instance>' como o distribuidor para '\<Server>\<Instance>'. Erro 18483: Não foi possível estabelecer conexão com o servidor '\<Server>\<Instance>', porque 'distributor_admin' não está definido como um logon remoto no servidor. Verifique se especificou o nome de logon correto. %.*ls.

## <a name="cause"></a>Causa

Quando você implanta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base em uma imagem de disco rígido de outro computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, o nome da rede do computador de imagem é retido na nova instalação. O nome incorreto da rede causa uma falha na configuração do distribuidor de replicação. O mesmo problema ocorrerá se você renomear o computador após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="user-action"></a>Ação do usuário

Para resolver esse problema, substitua o nome do servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo nome correto da rede do computador. Para fazer isso, siga estas etapas:

1. Faça logon no computador em que você implantou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base na imagem de disco e execute a seguinte instrução Transact-SQL no SSMS:

    ```sql
    -- Use the Master database
    USE master
    GO

    -- Declare local variables
    DECLARE @serverproperty_servername varchar(100),
    @servername varchar(100);

    -- Get the value returned by the SERVERPROPERTY system function
    SELECT @serverproperty_servername = CONVERT(varchar(100), SERVERPROPERTY('ServerName'));

    -- Get the value returned by @@SERVERNAME global variable
    SELECT @servername = CONVERT(varchar(100), @@SERVERNAME);

    -- Drop the server with incorrect name
    EXEC sp_dropserver @server=@servername;

    -- Add the correct server as a local server
    EXEC sp_addserver @server=@serverproperty_servername, @local='local';
    ```

2. Reinicie o computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
3. Para verificar se o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o nome da rede do computador são os mesmos, execute a seguinte instrução Transact-SQL:

    ```sql
    SELECT @@SERVERNAME, SERVERPROPERTY('ServerName');
    ```

## <a name="more-information"></a>Mais informações

Use a variável global `@@SERVERNAME` ou a função `SERVERPROPERTY`('ServerName') no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para encontrar o nome da rede do computador que está executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A propriedade ServerName da função `SERVERPROPERTY` relata automaticamente a alteração no nome da rede do computador quando você reinicia o computador e o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A variável global `@@SERVERNAME` retém o nome do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] original até que o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja redefinido manualmente.

### <a name="steps-to-reproduce-the-problem"></a>Etapas necessárias para reproduzir o problema

No computador em que você implantou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base em uma imagem de disco, siga estas etapas:

1. Inicie o [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)].
2. No **Pesquisador de Objetos**, expanda o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
3. Clique com o botão direito do mouse na pasta **Replicação**, clique em **Configurar Replicação de distribuição** e clique em **Configurar Publicação, Assinantes e Distribuição**.
4. Na caixa de diálogo do Assistente para **Configurar a Distribuição**, clique em **Avançar**.
5. Na caixa de diálogo **Distribuidor**, clique nela para selecionar a '\<**Server**>\<**Instance**>' que funcionará como o próprio distribuidor. O SQL Server criará um botão de opção de log e banco de dados de distribuição. Depois, clique em **Avançar**.
6. Na caixa de diálogo **Iniciar SQL Server Agent**, clique em **Avançar**.
7. Na caixa de diálogo **Pasta de Instantâneo**, clique em **Avançar**.

    > [!NOTE]
    > Se você receber uma mensagem para confirmar o caminho da pasta de instantâneo, clique em **Sim**.
8. Na caixa de diálogo **Banco de Dados de Distribuição**, clique em **Avançar**.
9. Na caixa de diálogo **Publicadores**, clique em **Avançar**.
10. Na caixa de diálogo **Ações do Assistente**, clique em **Avançar**.
11. Na caixa de diálogo **Concluir o Assistente**, clique em **Concluir**.

## <a name="see-also"></a>Consulte também

- [Renomear um computador que hospeda uma instância autônoma do SQL Server](/sql/database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server)
- [@@SERVERNAME (Transact-SQL)](/sql/t-sql/functions/servername-transact-sql)
- [SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)
- [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)
