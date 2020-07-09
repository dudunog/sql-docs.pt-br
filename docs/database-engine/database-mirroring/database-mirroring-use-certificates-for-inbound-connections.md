---
title: Usar certificados para conexão de entrada
description: Descreve as etapas para configuração de instâncias de servidor a fim de usar certificados para autenticar conexões de entrada para espelhamento de banco de dados.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- inbound connections
- database mirroring [SQL Server], security
ms.assetid: 5d48bb98-61f0-4b99-8f1a-b53f831d63d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8193710d3bd5e1fc132e10766c0f3440f1b7a422
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754722"
---
# <a name="database-mirroring---use-certificates-for-inbound-connections"></a>Espelhamento de Banco de Dados – usar certificados para conexões de entrada
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esse tópico descreve as etapas para configuração de instâncias de servidor a fim de usar certificados para autenticar conexões de entrada para espelhamento de banco de dados. Antes de poder configurar conexões de entrada, devem ser configuradas conexões de saída em cada instância de servidor. Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
 O processo de configuração conexões de entrada envolve as seguintes etapas gerais:  
  
1.  Crie um logon para outro sistema.  
  
2.  Crie um usuário para aquele logon.  
  
3.  Obtenha o certificado para o ponto de extremidade de espelhamento da outra instância do servidor.  
  
4.  Associe o certificado ao usuário criado na etapa 2.  
  
5.  Conceda permissão CONNECT no logon para aquele ponto de extremidade de espelhamento.  
  
 Se houver uma testemunha, deve-se configurar também conexões de entrada para ela. Isso requer configuração de logons, usuários e certificados para a testemunha nos dois parceiros, e vice-versa.  
  
 O procedimento a seguir descreve em detalhes essas etapas. Para cada etapa, o processo fornece um exemplo para configurar a instância do servidor em um sistema chamado de HOST_A. A seção de exemplo mostra as mesmas etapas para uma outra instância do servidor em um sistema chamado de HOST_B.  
  
### <a name="to-configure-server-instances-for-inbound-mirroring-connections-on-host_a"></a>Para configurar instâncias de servidor para conexões de espelhamento de entrada (em HOST_A)  
  
1.  Crie um logon para o outro sistema.  
  
     O exemplo a seguir cria um logon para o sistema, HOST_B, no banco de dados **master** da instância do servidor em HOST_A; nesse exemplo, o logon é chamado de `HOST_B_login`. Substitua a senha de exemplo por uma senha de sua escolha.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login   
       WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
     Para obter mais informações, veja [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md).  
  
     Para exibir os logons nessa instância de servidor, é possível usar a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```  
    SELECT * FROM sys.server_principals  
    ```  
  
     Para obter mais informações, veja [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
2.  Crie um usuário para aquele logon.  
  
     O exemplo a seguir cria um usuário, `HOST_B_user`, para o logon criado na etapa anterior.  
  
    ```  
    USE master;  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
     Para obter mais informações, consulte [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
     Para exibir os usuários nessa instância de servidor é possível usar a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```  
    SELECT * FROM sys.sysusers;  
    ```  
  
     Para obter mais informações, veja [sys.sysusers &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md).  
  
3.  Obtenha o certificado para o ponto de extremidade de espelhamento da outra instância do servidor.  
  
     Se ainda não tiver feito isso ao configurar as conexões de saída, obtenha uma cópia do certificado para o ponto de extremidade da instância de servidor remoto. Para fazer isso, faça backup do certificado na instância de servidor, conforme descrito em [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md). Ao copiar um certificado para outro sistema, use um método de cópia seguro. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
     Para obter mais informações, veja [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md).  
  
4.  Associe o certificado ao usuário criado na etapa 2.  
  
     O exemplo a seguir associa o certificado de HOST_B a seu usuário em HOST_A.  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
     Para obter mais informações, consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md).  
  
     Para exibir os certificados nessa instância de servidor, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```  
    SELECT * FROM sys.certificates  
    ```  
  
     Para obter mais informações, veja [sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md).  
  
5.  Conceda permissão CONNECT no logon para o ponto de extremidade de espelhamento remoto.  
  
     Por exemplo, para conceder permissão em HOST_A para a instância de servidor remoto em HOST_B para conexão com seu logon local – ou seja, para conexão com `HOST_B_login`– use as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```  
    USE master;  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
     Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
 Isso completa a configuração da autenticação de certificado para que HOST_B faça o logon para HOST_A.  
  
 Agora é preciso executar as etapas de entrada equivalentes para HOST_A em HOST_B. Essas etapas são ilustradas na porção de entrada do exemplo, na seção Exemplo, abaixo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como configurar HOST_B para conexões de entrada.  
  
> [!NOTE]  
>  Este exemplo usa um arquivo de certificado que contém o certificado HOST_A criado por um snippet de código em [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
```  
USE master;  
--On HOST_B, create a login for HOST_A.  
CREATE LOGIN HOST_A_login WITH PASSWORD = 'AStrongPassword!@#';  
GO  
--Create a user, HOST_A_user, for that login.  
CREATE USER HOST_A_user FOR LOGIN HOST_A_login  
GO  
--Obtain HOST_A certificate. (See the note   
--   preceding this example.)  
--Asscociate this certificate with the user, HOST_A_user.  
CREATE CERTIFICATE HOST_A_cert  
   AUTHORIZATION HOST_A_user  
   FROM FILE = 'C:\HOST_A_cert.cer';  
GO  
--Grant CONNECT permission for the server instance on HOST_A.  
GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO HOST_A_login  
GO  
```  
  
 Se você pretende executar em modo de alta segurança com failover automático, você deve repetir as mesmas etapas de configuração para configurar a testemunha para conexões de saída e de entrada.  
  
 Para obter informações sobre como criar um banco de dados espelho, incluindo um exemplo de Transact-SQL, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 Para obter um exemplo do Transact-SQL de estabelecimento uma sessão de modo de alto desempenho, veja [Exemplo: Configurando o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Ao copiar um certificado para outro sistema, use um método de cópia seguro. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
