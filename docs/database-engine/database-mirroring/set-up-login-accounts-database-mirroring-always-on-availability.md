---
title: Configurar contas de logon (espelhamento e grupos de disponibilidade)
description: Configure contas de logon para acessar o ponto de extremidade de espelhamento do banco de dados de um espelho de banco de dados ou em um grupo de disponibilidade Always On.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea62f1f934527ce40e2b5fe2f03b8b6c1b8e49bc
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641970"
---
# <a name="set-up-login-accounts---database-mirroring-always-on-availability"></a>Configurar contas de logon – disponibilidade AlwaysOn do espelhamento de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Para que duas instâncias de servidor se conectem ao [ponto de extremidade de espelhamento de banco de dados](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) entre si, é necessário acesso mútuo entre as conta de logon de cada instância. Além disso, cada conta de logon exige a permissão de conexão com o ponto de extremidade do Espelhamento de Banco de Dados da outra instância.  
  
 O impacto desse requisito depende das instâncias de servidor executadas como a mesma conta de usuário do domínio:  
  
-   Se as instâncias de servidor forem executadas como a mesma conta de usuário do domínio, os logons de usuário corretos existirão automaticamente em ambos os bancos de dados **mestres** . Isso simplifica a configuração de segurança do Espelhamento de Banco de Dados e de Grupos de Disponibilidade AlwaysOn.  
  
-   Se as instâncias de servidor forem executadas como contas de usuário diferentes, os logons de usuário na instância de servidor que hospeda o servidor principal ou a réplica principal deverão ser reproduzidos manualmente na instância de servidor que hospeda o servidor espelho ou em todas as instâncias de servidor que hospedem uma réplica secundária. Para obter mais informações, consulte [Criar um logon para uma conta diferente](#CreateLogin) e [Conceder permissão de conexão](#GrantConnect), posteriormente neste tópico.  
  
    > [!IMPORTANT]  
    >  Para criar um ambiente mais seguro, procure usar contas de domínio separadas para cada instância do servidor.  
  
##  <a name="create-a-login-for-a-different-account"></a><a name="CreateLogin"></a> Criar um logon para uma conta diferente  
 Se duas instâncias de servidor forem executadas como contas diferentes, o administrador do sistema deve usar a instrução CREATE LOGIN [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar um logon para a conta de serviço de inicialização da instância remota para cada instância do servidor. Para obter mais informações, veja [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md).  
  
> [!IMPORTANT]  
>  Se você executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma conta fora do domínio, deverá usar certificados. Para obter mais informações, consulte [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
 Por exemplo, para a instância de servidor sqlA, executada em loginA, conectar-se à instância de servidor sqlB, executada no loginB, o loginA deve existir no sqlB e loginB, loginA deve existir no sqlA. Além disso, para uma sessão de espelhamento de banco de dados que inclui uma instância de servidor testemunha (sqlC) e na qual as três instâncias de servidor são executadas em contas de domínio diferentes, devem ser criados os seguintes logons:  
  
|Na instância...|Crie logons para e conceda permissão de conexão para ...|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB e sqlC|  
|sqlB|sqlA e sqlC|  
|sqlC|sqlA e sqlB|  
  
> [!NOTE]  
>  É possível conectar-se com a conta de serviço de rede usando a conta da máquina em vez de um usuário de domínio. Se a conta da máquina for usada, ela deve ser adicionada como um usuário na outra instância de servidor.  
  
##  <a name="grant-connect-permission"></a><a name="GrantConnect"></a> Conceder permissão de conexão  
 Quando um logon tiver sido criado em uma instância de servidor, deve ser concedida permissão para que ele se conecte com o ponto de extremidade de espelhamento de banco de dados da instância de servidor. O administrador do sistema concede a permissão de conexão usando uma instrução GRANT [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md).  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
