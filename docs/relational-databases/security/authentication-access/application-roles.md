---
title: Funções de aplicativo | Microsoft Docs
description: Use funções de aplicativo para habilitar o acesso a dados somente aos usuários que se conectam por um aplicativo específico no SQL Server.
ms.custom: ''
ms.date: 08/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- application roles [SQL Server], about application roles
- principals [SQL Server], application roles
- credentials [SQL Server], roles
- application roles [SQL Server]
- roles [SQL Server], application
- permissions [SQL Server], roles
- users [SQL Server], application roles
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: dca18b8a-ca03-4b7f-9a46-8474d5b66f76
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01d9a3825b2972313602cbc077c0da501868c712
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332205"
---
# <a name="application-roles"></a>Funções de aplicativo
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Uma função de aplicativo é uma entidade de banco de dados que permite que um aplicativo execute com suas próprias permissões de usuário. As funções de aplicativos podem ser usadas para habilitar acesso a dados específicos somente aos usuários que se conectam por um aplicativo específico. Diferentemente de funções de banco de dados, funções de aplicativo não contêm membros e são inativas por padrão. Funções de aplicativo são habilitadas usando **sp_setapprole**, que requer uma senha. Como as funções de aplicativo são uma entidade de nível de banco de dados, elas só podem acessar outros bancos de dados através de permissões concedidas nesses bancos de dados como **convidado**. Portanto, qualquer banco de dados no qual o **convidado** tenha sido desabilitado estará inacessível a funções de aplicativo em outros bancos de dados.  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], funções de aplicativo não podem acessar metadados de nível de servidor porque eles não estão associados a uma entidade de nível de servidor. Para desabilitar essa restrição e assim permitir que funções de aplicativo acessem metadados de nível de servidor, defina o sinalizador global 4616. Para obter mais informações, consulte [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) e [DBCC TRACEON &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md).  
  
## <a name="connecting-with-an-application-role"></a>Conectando com uma função de aplicativo  
 As etapas seguintes compõem o processo pelo qual uma função de aplicativo alterna contextos de segurança:  
  
1.  Um usuário executa um aplicativo cliente.  
  
2.  O aplicativo cliente conecta com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o usuário.  
  
3.  O aplicativo executa o procedimento armazenado **sp_setapprole** com uma senha somente conhecida pelo aplicativo.  
  
4.  Se o nome de função de aplicativo e a senha forem válidos, a função de aplicativo será habilitada.  
  
5.  Nesse momento, a conexão perde as permissões de usuário e assume as permissões da função de aplicativo.  

 As permissões adquiridas pela função de aplicativo permanecem em efeito durante a conexão.  
  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a única maneira de um usuário readquirir seu contexto de segurança original depois de iniciar uma função de aplicativo é desconectar e conectar-se novamente com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o **sp_setapprole** tem uma opção que cria um cookie. O cookie contém informações de contexto anteriores à habilitação da função de aplicativo. O cookie pode ser usado por **sp_unsetapprole** para reverter a sessão a seu contexto original. Para obter mais informações sobre essa nova opção e um exemplo, consulte [sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
> [!IMPORTANT]  
>  A opção ODBC **criptografia** não tem suporte no **SqlClient**. Ao transmitir informações confidenciais pela rede, use o protocolo TLS, anteriormente conhecido como SSL (Secure Sockets Layer) ou IPsec para criptografar o canal. Se você deve persistir credenciais no aplicativo cliente, criptografe as credenciais usando as funções API de criptografia. No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, o parâmetro *senha* é armazenado como um hash de mão única.  
  
## <a name="related-tasks"></a>Related Tasks  
  
| Tarefa | Type |
| ---- | ---- |
|Criar uma função de aplicativo.|[Criar uma função de aplicativo](../../../relational-databases/security/authentication-access/create-an-application-role.md) e [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)|  
|Alterar uma função de aplicativo.|[ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-application-role-transact-sql.md)|  
|Excluir uma função de aplicativo.|[DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-application-role-transact-sql.md)|  
|Usando uma função de aplicativo.|[sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
