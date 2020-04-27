---
title: Solução de problemas de usuários órfãos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63035644"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>Solução de problemas de usuários órfãos (SQL Server)
  Para fazer logon em uma instância do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma entidade deve ter um logon válido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse logon é usado no processo de autenticação que verifica se a entidade tem permissão para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons em uma instância de servidor são visíveis na exibição de catálogo **Sys. server_principals** e na exibição de compatibilidade **Sys. syslogins** .  
  
 Os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acessam bancos de dados individuais usando um usuário do banco de dados mapeado para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Há duas exceções a essa regra:  
  
-   A conta Convidado.  
  
     Essa é uma conta que, quando habilitada no banco de dados, habilita os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não mapeados para um usuário do banco de dados para acessar o banco de dados como um usuário convidado.  
  
-   Associação de grupo do Microsoft Windows.  
  
     Um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um usuário do Windows poderá acessar um banco de dados se esse usuário for membro de um grupo do Windows que também seja um usuário no banco de dados.  
  
 Informações sobre o mapeamento de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um usuário do banco de dados são armazenadas no banco de dados. Isso inclui o nome do usuário do banco de dados e o SID do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente. As permissões desse usuário de banco de dados são usadas para autorização no banco de dados.  
  
 Um usuário de banco de dados para o qual o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente não está definido ou está definido incorretamente em uma instância do servidor não pode fazer logon na instância. Esse usuário é um *usuário órfão* do banco de dados nessa instância do servidor. Um usuário do banco de dados torna-se órfão se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente for descartado. Além disso, um usuário de banco de dados pode se tornar órfão após um banco de dados ser restaurado ou anexado a uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A condição de órfão pode ocorrer se o usuário do banco de dados for mapeado para um SID que não esteja presente na nova instância do servidor.  
  
> [!NOTE]  
>  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon não pode acessar um banco de dados no qual ele não tem um usuário de banco de dados correspondente, a menos que o **convidado** esteja habilitado nesse banco de dados. Para obter informações sobre como criar uma conta de usuário de banco de dados, consulte [Create user &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="to-detect-orphaned-users"></a>Para detectar usuários órfãos  
 Para detectar usuários órfãos, execute as seguintes instruções Transact-SQL:  
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 A saída lista os usuários e os SIDs (identificadores de segurança) correspondentes no banco de dados atual que não estão vinculados a um logon de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sp_change_users_login &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
> [!NOTE]  
>  **sp_change_users_login** não pode ser usado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com logons criados no Windows.  
  
## <a name="to-resolve-an-orphaned-user"></a>Para resolver um usuário órfão  
 Para resolver um usuário órfão, use o seguinte procedimento:  
  
1.  O comando a seguir revincula a conta de logon do servidor especificada por *<login_name>* com o usuário do banco de dados especificado por *<database_user *>.  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     Para obter mais informações, consulte [sp_change_users_login &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
2.  Depois que você executar o código na etapa anterior, o usuário poderá acessar o banco de dados. Em seguida, o usuário pode alterar a senha do *<login_name>* conta de logon usando o procedimento armazenado **sp_password** , da seguinte maneira:  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  Somente logons com a permissão ALTER ANY LOGIN podem alterar a senha do logon de outro usuário. Porém, somente membros da função **sysadmin** podem modificar senhas de membros da função **sysadmin** .  
  
    > [!NOTE]  
    >  **sp_password** não pode ser usada [!INCLUDE[msCoName](../../includes/msconame-md.md)] para contas do Windows. Usuários que se conectam a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pela da conta de rede do Windows são autenticados pelo Windows; portanto, suas senhas só podem ser alteradas no Windows.  
  
     Para obter mais informações, consulte [sp_password &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR usuário &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CRIAR logon &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-login-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_change_users_login](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_addlogin](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_password](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sys. sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [sys. syslogins &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
