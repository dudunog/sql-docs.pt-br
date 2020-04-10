---
title: 'Como fazer: Conectar usando a Autenticação do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 066c58d9ee72f1160b84d4f4a3de9f7156a47d6e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916498"
---
# <a name="how-to-connect-using-windows-authentication"></a>Como fazer: Conectar usando a Autenticação do Windows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Por padrão, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usam a Autenticação do Windows para se conectar ao SQL Server. É importante observar que, na maioria dos cenários, isso significa que a identidade do processo ou do thread do servidor Web (se o servidor Web estiver usando representação) será usada para a conexão ao servidor e não a identidade de um usuário final.  
  
Os seguintes pontos devem ser considerados ao usar a Autenticação do Windows para se conectar ao SQL Server:  
  
-   As credenciais usadas na execução do processo (ou thread) do servidor Web devem estar mapeadas a um logon válido do SQL Server para que a conexão seja estabelecida.  
  
-   Se o SQL Server e o servidor Web estiverem em computadores diferentes, o SQL Server deve ser configurado para permitir conexões remotas.  
  
> [!NOTE]  
> Atributos de conexão como *Database* e *ConnectionPooling* podem ser definidas ao estabelecer uma conexão. Para obter uma lista completa dos atributos de conexão com suporte, consulte [Connection Options](../../connect/php/connection-options.md).  
  
A Autenticação do Windows deve ser usada para se conectar ao SQL Server sempre que possível, pelos seguintes motivos:  
  
-   Nenhuma credencial é passada pela rede durante a Autenticação; nomes de usuário e senhas não são incorporadas na cadeia de conexão de banco de dados. Isso significa que usuários mal-intencionados ou invasores não podem obter as credenciais monitorando a rede ou exibindo cadeias de conexão nos arquivos de configuração.  
  
-   Os usuários estão sujeitos ao gerenciamento de contas centralizado e políticas de segurança, como períodos de validade da senha, comprimento mínimo da senha e bloqueio de conta após várias solicitações de logon inválidas, são impostas.  
  
Se a Autenticação do Windows não for uma opção prática, confira [Como conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa o driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]com Autenticação do Windows para se conectar a uma instância local do SQL Server. Depois que a conexão tiver sido estabelecida, o servidor será consultado para o logon do usuário que está acessando o banco de dados.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída é gravada no navegador quando o exemplo é executado do navegador.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa o driver PDO_SQLSRV para executar a mesma tarefa do exemplo anterior.  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Como: conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Como: criar um logon do SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Como: criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Gerenciando usuários, funções e logons](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Separação do Esquema de Usuário](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Conceder permissões de objeto (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
