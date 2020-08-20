---
description: Definir um banco de dados como modo de usuário único
title: Definir um banco de dados como modo de usuário único | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], database option
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 591a2d22a603c51f44bdfa16d4072e6b9ad36c73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471124"
---
# <a name="set-a-database-to-single-user-mode"></a>Definir um banco de dados como modo de usuário único
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como configurar um banco de dados definido pelo usuário no modo de usuário único no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O modo de usuário único especifica que apenas um usuário pode acessar o banco de dados por vez e, normalmente é usado para ações de manutenção.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para definir um banco de dados como modo de usuário único, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se outros usuários estiverem conectados ao banco de dados no momento em que você configurar o banco de dados como modo de usuário único, as conexões deles ao banco de dados serão fechadas sem aviso.  
  
-   O banco de dados permanece em modo de usuário único mesmo se o usuário que definiu a opção fizer logoff. Nesse momento, um usuário diferente, mas somente um, poderá se conectar ao banco de dados.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de definir o banco de dados como SINGLE_USER, verifique se a opção AUTO_UPDATE_STATISTICS_ASYNC está definida como OFF. Quando esta opção está definida como ON, o thread em segundo plano usado para a atualização de estatísticas estabelece uma conexão com o banco de dados e não será possível acessar o banco de dados em modo de usuário único. Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>Para definir um banco de dados como modo de usuário único  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Clique com o botão direito do mouse no banco de dados a ser alterado e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , clique na página **Opções** .  
  
4.  Da opção **Restringir o Acesso** , selecione **Simples**.  
  
5.  Se outros usuários estiverem conectados ao banco de dados, uma mensagem **Conexões Abertas** será exibida. Para alterar a propriedade e fechar todas as outras conexões, clique em **Sim**.  
  
 Também é possível definir o banco de dados como acesso múltiplo ou restrito usando esse procedimento. Para obter mais informações sobre as opções de Restringir o Acesso, veja [Propriedades de banco de dados &#40;Página Opções&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>Para definir um banco de dados como modo de usuário único  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo define o banco de dados como o modo `SINGLE_USER` para obter acesso exclusivo. Em seguida, o exemplo define o estado do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `READ_ONLY` e retorna o acesso ao banco de dados para todos os usuários. A opção de término `WITH ROLLBACK IMMEDIATE` é especificada na primeira instrução `ALTER DATABASE` . Isso levará todas as transações incompletas a serem revertidas e qualquer outra conexão com o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a ser desconectada imediatamente.  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../relational-databases/databases/codesnippet/tsql/set-a-database-to-single_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
