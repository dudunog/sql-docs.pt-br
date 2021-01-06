---
title: Instância do servidor principal (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
description: Uma descrição da página 'Instância do Servidor Principal' do Assistente de 'Configurar Segurança de Espelhamento do Banco de Dados' no SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fc2a6f30a4832fb19856b19eb47dde63e449bd20
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97644225"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>Instância do servidor principal (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use essa página para especificar informações sobre a instância de servidor principal do banco de dados. O banco de dados principal é a cópia do banco de dados que dá início à sessão de espelhamento. Após o início da sessão, o banco de dados principal é a cópia do banco de dados que aceita as mudanças feitas pelo usuário. (Quando ocorre um failover, as funções principal e de espelhamento são trocadas. Dessa forma, o banco de dados principal inicial pode não permanecer como banco de dados principal.)  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Instância do servidor principal**  
 Como o espelhamento de banco de dados do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é sempre configurado no servidor principal, a instância do servidor atual é sempre a instância do servidor principal.  
  
 **Porta do ouvinte**  
 O comportamento dessa opção depende de o ponto de extremidade do espelhamento existir nessa instância do servidor, como segue:  
  
-   Se não houver porta do ouvinte na instância do servidor, o número da porta 5022 será exibido na caixa de texto **Porta** . Você pode usar qualquer número de porta disponível, como 7022.  
  
-   Quando o ponto de extremidade do espelhamento já existir, o número da porta daquele ponto de extremidade será exibido. Se for necessário alterar a porta, use um comando ALTER ENDPOINT. Para obter mais informações, consulte [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
> [!NOTE]  
>  É necessário um número de porta.  
  
 **Nome do ponto de extremidade**  
 Se o ponto de extremidade de espelhamento existir para essa instância do servidor, o nome de ponto de extremidade será exibido aqui. Se o ponto de extremidade não existir, você poderá especificar o nome do ponto de extremidade.  
  
 **Criptografar dados enviados por esse ponto de extremidade**  
 Por padrão, a criptografia está habilitada. Quando habilitada, a criptografia é necessária (não tem meramente um suporte) e usa os valores padrão de todas as opções de criptografia. Para obter mais informações, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Para desabilitar a criptografia, desmarque a caixa de seleção. Para habilitar a criptografia novamente, marque a caixa de seleção.  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
