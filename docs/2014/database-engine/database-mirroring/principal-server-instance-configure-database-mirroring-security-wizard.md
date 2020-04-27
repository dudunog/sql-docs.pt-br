---
title: Instância do servidor principal (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4fde67fc6b38e81c7367ee1e298439810b0b35c6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754566"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>Instância do servidor principal (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
  Use essa página para especificar informações sobre a instância de servidor principal do banco de dados. O banco de dados principal é a cópia do banco de dados que dá início à sessão de espelhamento. Após o início da sessão, o banco de dados principal é a cópia do banco de dados que aceita as mudanças feitas pelo usuário. (Quando ocorre um failover, as funções principal e de espelhamento são trocadas. Dessa forma, o banco de dados principal inicial pode não permanecer como banco de dados principal.)  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Instância do servidor principal**  
 Como o espelhamento de banco de dados do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é sempre configurado no servidor principal, a instância do servidor atual é sempre a instância do servidor principal.  
  
 **Porta do Ouvinte**  
 O comportamento dessa opção depende de o ponto de extremidade do espelhamento existir nessa instância do servidor, como segue:  
  
-   Se não houver porta do ouvinte na instância do servidor, o número da porta 5022 será exibido na caixa de texto **Porta** . Você pode usar qualquer número de porta disponível, como 7022.  
  
-   Quando o ponto de extremidade do espelhamento já existir, o número da porta daquele ponto de extremidade será exibido. Se for necessário alterar a porta, use um comando ALTER ENDPOINT. Para obter mais informações, consulte [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
> [!NOTE]  
>  É necessário um número de porta.  
  
 **Nome do ponto de extremidade**  
 Se o ponto de extremidade de espelhamento existir para essa instância do servidor, o nome de ponto de extremidade será exibido aqui. Se o ponto de extremidade não existir, você poderá especificar o nome do ponto de extremidade.  
  
 **Criptografar dados enviados por esse ponto de extremidade**  
 Por padrão, a criptografia está habilitada. Quando habilitada, a criptografia é necessária (não tem meramente um suporte) e usa os valores padrão de todas as opções de criptografia. Para obter mais informações, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
 Para desabilitar a criptografia, desmarque a caixa de seleção. Para habilitar a criptografia novamente, marque a caixa de seleção.  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Propriedades do banco de dados &#40;página espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para autenticação do Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Iniciar o monitor de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
