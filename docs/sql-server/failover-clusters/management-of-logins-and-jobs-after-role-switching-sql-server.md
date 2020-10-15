---
title: Gerenciar logons e trabalhos após o failover de espelho
description: Saiba como gerenciar logons e trabalhos após o failover de seu banco de dados espelhado do banco de dados primário para o secundário.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- role switching [SQL Server]
ms.assetid: fc2fc949-746f-40c7-b5d4-3fd51ccfbd7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 234657a06ca2162bffc9448a1424820ead00f0c3
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988332"
---
# <a name="management-of-logins-and-jobs-after-role-switching-sql-server"></a>Administração de logons e trabalhos depois de troca de funções (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Ao implantar uma solução de alta disponibilidade ou de recuperação de desastres para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é importante reproduzir informações relevantes que são armazenadas para o banco de dados nos bancos de dados **master** ou **msdb** . Normalmente, as informações relevantes incluem os trabalhos do banco de dados principal/primário e os logons de usuários ou de processos que precisam se conectar ao banco de dados. É necessário duplicar essas informações em qualquer instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda um banco de dados secundário/espelho. Se for possível, após a troca de funções, o melhor é reproduzir de forma programática as informações do banco de dados primário/principal.  
  
## <a name="logins"></a>Logons  
 Em cada instância de servidor que hospeda uma cópia do banco de dados, você precisa reproduzir os logons que têm permissão para acessar o banco de dados principal. Quando a função principal/primária for alternada, somente os usuários cujos logons existirem na nova instância de servidor principal/primária poderão acessar o novo banco de dados principal/primário. Os usuários cujos logons não estão definidos na nova instância de servidor principal/primária ficam órfãos e não podem acessar o banco de dados.  
  
 Se um usuário ficar órfão, crie o logon na nova instância de servidor primária/principal e execute [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md). Para obter mais informações, consulte [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md).  
  
###  <a name="logins-of-applications-that-use-sql-server-authentication-or-a-local-windows-login"></a><a name="SSauthentication"></a> Os logons dos aplicativos que usam a autenticação do SQL Server ou Logon local do Windows  
 Se um aplicativo usar a autenticação do SQL Server ou um logon local do Windows, as SIDs incompatíveis poderão impedir que o logon do aplicativo seja resolvido em uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As SIDs incompatíveis fazem o logon se tornar um usuário órfão na instância do servidor remoto. Esse problema pode ocorrer quando um aplicativo se conectar a um banco de dados espelhado ou de envio de logs depois de um failover ou a um banco de dados de assinante de replicação que foi inicializado de um backup.  
  
 Para evitar esse problema, recomendamos que você tome medidas preventivas quando configurar esse aplicativo para usar um banco de dados que seja hospedado por uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A prevenção envolve transferir os logons e as senhas da instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como evitar esse problema, confira o artigo da base de conhecimento 918992 –[Como transferir logons e senhas entre instâncias do SQL Server](https://support.microsoft.com/kb/918992/)).  
  
> [!NOTE]  
>  Esse problema afeta contas locais do windows em computadores diferentes. No entanto, esse problema não ocorre para contas de domínio porque o SID será o mesmo em cada computador.  
  
 Para obter mais informações, consulte [Usuários órfãos com espelhamento de banco de dados e envio de logs](/archive/blogs/sqlserverfaq/orphaned-users-with-database-mirroring-and-log-shipping) (um blog do mecanismo de banco de dados).  
  
## <a name="jobs"></a>Trabalhos  
 Trabalhos, tais como trabalhos de backup, requerem consideração especial. Em geral, após uma troca de funções, o proprietário do banco de dados ou administrador do sistema deve recriar os trabalhos para o novo banco de dados primário/principal.  
  
 Quando a instância de servidor primária/principal anterior estiver disponível, será preciso excluir os trabalhos originais nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os trabalhos no banco de dados espelho atual apresentam falhas porque o banco de dados está no estado RESTORING, tornando-o indisponível.  
  
> [!NOTE]  
>  Diferentes instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderiam ser configuradas de forma diferente, com diferentes letras de unidade de fita ou algo semelhante. Os trabalhos de cada parceiro devem permitir essas diferenças.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
