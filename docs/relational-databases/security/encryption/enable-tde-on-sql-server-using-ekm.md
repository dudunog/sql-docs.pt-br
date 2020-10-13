---
title: Habilitar TDE no SQL Server usando EKM | Microsoft Docs
description: Habilite a Transparent Data Encryption no SQL Server para proteger uma chave de banco de dados usando uma chave assimétrica em um módulo de gerenciamento de chave extensível com o Transact-SQL.
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], TDE using an EKM
- TDE, EKM how to
- EKM, TDE how to
- Transparent Data Encryption, using EKM
ms.assetid: b892e7a7-95bd-4903-bf54-55ce08e225af
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 74c27195e3adbb39714a2df23ef041615262ffc2
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867855"
---
# <a name="enable-tde-on-sql-server-using-ekm"></a>Habilitar TDE no SQL Server usando EKM
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este artigo descreve como habilitar a TDE (Transparent Data Encryption) no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para proteger uma chave de criptografia de banco de dados usando uma chave assimétrica armazenada em um módulo EKM (gerenciamento extensível de chaves) com o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 A TDE criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de chave de criptografia de banco de dados. A chave de criptografia do banco de dados também pode ser protegida usando um certificado, protegido pela chave mestra do banco de dados mestre. Para obter mais informações sobre como proteger a chave de criptografia do banco de dados usando a chave mestra de banco de dados, veja [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md). Para obter informações sobre como configurar a TDE quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está em execução em uma VM do Azure, veja [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md). Para obter informações sobre como configurar a TDE usando uma chave no Cofre de Chaves do Azure, veja [Usar o Conector do SQL Server com recursos de criptografia do SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md). 

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Você deve ser um usuário com altos privilégios (como um administrador do sistema) para criar uma chave de criptografia de banco de dados e criptografar um banco de dados. É necessário que esse usuário possa ser autenticado pelo módulo EKM.  
  
-   Ao iniciar, o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve abrir o banco de dados. Para fazer isso, você deverá criar uma credencial que será autenticada pelo EKM, que adicioná-la ao logon baseado em uma chave assimétrica. Os usuários não podem entrar com esse logon, mas o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] poderá se autenticar com o dispositivo de EKM.  
  
-   Se a chave assimétrica armazenada no módulo EKM for perdida, não será possível abrir o banco de dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o provedor de EKM permitir o backup da chave assimétrica, crie o backup e armazene-o em um local seguro.  
  
-   As opções e os parâmetros exigidos por seu provedor de EKM podem diferir do que é fornecido no exemplo de código abaixo. Para obter mais informações, consulte seu provedor de EKM.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Este artigo usa as seguintes permissões:  
  
-   Para alterar uma opção de configuração e executar a instrução RECONFIGURE, você deve ter a permissão em nível de servidor ALTER SETTINGS. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
-   Requer a permissão ALTER ANY CREDENTIAL.  
  
-   Requer a permissão ALTER ANY LOGIN.  
  
-   Requer a permissão CREATE ASYMMETRIC KEY.  
  
-   Requer a permissão CONTROL no banco de dados para criptografá-lo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-enable-tde-using-ekm"></a>Para habilitar a TDE usando EKM  
  
1.  Copie os arquivos fornecidos pelo provedor de EKM em um local apropriado no computador com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Neste exemplo, usamos a pasta **C:\EKM** .  
  
2.  Instale os certificados no computador, como requerido pelo provedor de EKM.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não fornece um provedor de EKM. Cada provedor de EKM pode ter procedimentos diferentes para instalar, configurar e autorizar os usuários.  Consulte a documentação do provedor de EKM para completar esta etapa.  
  
3.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
4.  Na barra Padrão, clique em **Nova Consulta**.  
  
5.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Enable advanced options.  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Create a cryptographic provider, which we have chosen to call "EKM_Prov," based on an EKM provider  
  
    CREATE CRYPTOGRAPHIC PROVIDER EKM_Prov   
    FROM FILE = 'C:\EKM_Files\KeyProvFile.dll' ;  
    GO  
  
    -- Create a credential that will be used by system administrators.  
    CREATE CREDENTIAL sa_ekm_tde_cred   
    WITH IDENTITY = 'Identity1',   
    SECRET = 'q*gtev$0u#D1v'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
    GO  
  
    -- Add the credential to a high privileged user such as your   
    -- own domain login in the format [DOMAIN\login].  
    ALTER LOGIN Contoso\Mary  
    ADD CREDENTIAL sa_ekm_tde_cred ;  
    GO  
    -- create an asymmetric key stored inside the EKM provider  
    USE master ;  
    GO  
    CREATE ASYMMETRIC KEY ekm_login_key   
    FROM PROVIDER [EKM_Prov]  
    WITH ALGORITHM = RSA_512,  
    PROVIDER_KEY_NAME = 'SQL_Server_Key' ;  
    GO  
  
    -- Create a credential that will be used by the Database Engine.  
    CREATE CREDENTIAL ekm_tde_cred   
    WITH IDENTITY = 'Identity2'   
    , SECRET = 'jeksi84&sLksi01@s'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
  
    -- Add a login used by TDE, and add the new credential to the login.  
    CREATE LOGIN EKM_Login   
    FROM ASYMMETRIC KEY ekm_login_key ;  
    GO  
    ALTER LOGIN EKM_Login   
    ADD CREDENTIAL ekm_tde_cred ;  
    GO  
  
    -- Create the database encryption key that will be used for TDE.  
    USE AdventureWorks2012 ;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM  = AES_128  
    ENCRYPTION BY SERVER ASYMMETRIC KEY ekm_login_key ;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE AdventureWorks2012   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
 Para saber mais, consulte o seguinte:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Transparent Data Encryption com o Banco de Dados SQL do Azure](/azure/azure-sql/database/transparent-data-encryption-tde-overview)  
  
