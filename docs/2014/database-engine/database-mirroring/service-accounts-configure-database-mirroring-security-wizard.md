---
title: Contas de serviço (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69877c6a20e37e012925185d0b807e9579066e35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754392"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Contas de Serviço (Assistente para Configurar Segurança de Espelhamento do Banco de Dados)
  Ao usar a Autenticação do Windows, se as instâncias de servidor usarem contas diferentes, especifique as contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas contas de serviço devem ser todas contas de domínio (nos mesmos domínios ou domínios confiáveis).  
  
 Se todas as instâncias de servidor usarem a mesma conta de domínio ou autenticação com base em certificação, deixe os campos em branco. Basta clicar em **Concluir**e o assistente configurará automaticamente as contas com base na conta do assistente atual.  
  
> [!IMPORTANT]  
>  Se os pontos de extremidade do espelhamento de banco de dados das instâncias de servidor estiverem configurados para usar certificados, então os campos de conta de serviço devem ser deixados em branco.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Beneficiário**  
 Especifique a conta de serviço da instância de servidor principal. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*Nome de usuário* DomainName  
  
 **Espelho**  
 Especifique a conta de serviço da instância de servidor espelho. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*Nome de usuário* DomainName  
  
 **Witness (testemunha)**  
 Especifique a conta de serviço da instância de servidor testemunha. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*Nome de usuário* DomainName  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do banco de dados &#40;página espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Iniciar o monitor de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [SQL Server de espelhamento de banco de dados &#40;&#41;](database-mirroring-sql-server.md)   
 [Configurar contas de logon para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
