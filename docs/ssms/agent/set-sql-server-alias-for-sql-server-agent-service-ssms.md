---
description: Como definir um alias do SQL Server para o serviço do SQL Server Agent
title: Como definir um alias do SQL Server para o serviço do SQL Server Agent
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: de8192ff8e15d2f599668116ce2026f492b55fd6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492040"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Como definir um alias do SQL Server para o serviço do SQL Server Agent

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Este tópico descreve como definir um alias do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para se conectar ao [!INCLUDE[ssDE](../../includes/ssde_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por padrão, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se conecta a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em pipes nomeados usando nomes dinâmicos de servidor que não exigem configuração adicional de cliente. Só será necessário configurar um alias de conexão com o servidor se você não estiver usando o transporte de rede padrão ou se estiver se conectando a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que escute em um pipe nomeado alternativo.  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não funcionará corretamente a menos que você selecione um alias referente à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Para definir um alias do SQL Server para o serviço do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] e expanda-a.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent**_server\_name_, em **Selecionar uma página**, selecione **Conexão**, e  
  
4.  Na caixa **Servidor de host local do alias** , digite o alias do servidor ao qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve se conectar.  
  
5.  Clique em **OK**.  
  
