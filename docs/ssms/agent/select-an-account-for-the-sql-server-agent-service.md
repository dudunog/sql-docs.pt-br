---
title: Selecionar uma conta para o Serviço do SQL Server Agent
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 05/04/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4356764f50b816a05e9bcfbfb294c65cdc8080fe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644688"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>Selecionar uma conta para o Serviço do SQL Server Agent

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A conta de inicialização do serviço define a conta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado, bem como suas permissões de rede. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado como uma conta de usuário especificada. Selecione uma conta para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no qual estão disponíveis as seguintes opções:  
  
-   **Conta interna**. Em uma lista, você pode escolher uma das seguintes contas de serviço Windows internas:  
  
    -   Conta**Sistema Local** . O nome desta conta é NT AUTHORITY\System. É uma conta poderosa, com acesso irrestrito a todos os recursos do sistema local. Ela é membro do grupo **Administradores** do Windows no computador local e, portanto, é membro da função de servidor fixa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin**  
  
        > [!IMPORTANT]  
        > A opção **conta Sistema Local** é fornecida apenas por questão de compatibilidade retroativa. A conta Sistema Local tem permissões de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não necessita. Evite executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent como a conta Sistema Local. Para maior segurança, use uma conta de domínio do Windows com as permissões listadas na seção "Permissões de contas de domínio do Windows", a seguir.  
  
-   **Esta conta**. Permite-lhe especificar a conta de domínio do Windows na qual deve ser executado o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Recomendamos escolher uma conta de usuário do Windows que não seja membro do grupo **Administradores** do Windows. Porém, há limitações ao uso de administração multisservidor quando a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não é membro do grupo **Administradores** local. Para obter mais informações, consulte 'Tipos de conta de serviço com suporte' a seguir neste tópico.  
  
## <a name="windows-domain-account-permissions"></a>Permissões de contas de domínio do Windows  
Para maior segurança, selecione **Esta conta**, que especifica uma conta de domínio do Windows. A conta de domínio do Windows que você especificar deve ter as seguintes permissões:  
  
-   Em todas as versões do Windows, permissão para efetuar logon como um serviço (SeServiceLogonRight)  
  
> [!NOTE]  
> A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve fazer parte do grupo Acesso Compatível Pré-Windows 2000 no controlador de domínio; caso contrário, os trabalhos de propriedade de usuários do domínio que não sejam membros do grupo Administradores do Windows falharão.  
  
-   Em servidores Windows, a conta em que o Serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado requer as permissões a seguir para poder dar suporte a proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
    -   Permissão para ignorar verificação completa (SeChangeNotifyPrivilege)  
  
    -   Permissão para substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
    -   Permissão para ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
    -   Permissão para acessar este computador pela rede (SeNetworkLogonRight)  
  
> [!NOTE]  
> Se a conta não tiver as permissões necessárias para dar suporte a proxies, apenas membros da função de servidor fixa **sysadmin** poderão criar trabalhos.  
  
> [!NOTE]  
> Para receber notificação de alertas do WMI, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve deter permissão para o namespace que contém os eventos do WMI e ALTER ANY EVENT NOTIFICATION.  
  
## <a name="sql-server-role-membership"></a>Associação a funções do SQL Server  
A conta em cujo nome é executado o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser membro das seguintes funções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   A conta deve ser membro da função de servidor fixa **sysadmin** .  
  
-   Para usar o processamento de trabalhos multisservidor, a conta deve ser membro da função de banco de dados **TargetServersRole** do **msdb** no servidor mestre.  
  
## <a name="supported-service-account-types"></a>Tipos de conta de serviço com suporte  
A tabela a seguir lista os tipos de conta do Windows que podem ser usadas para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Tipo de conta de serviço|Servidor não clusterizado|Servidor em cluster|Controlador de domínio (não clusterizado)|  
|------------------------|-------------------------|--------------------|--------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)] Conta de domínio do Windows (membro do grupo Administradores do Windows)|Com suporte|Com suporte|Com suporte|  
|Conta de domínio do Windows (não administrativa)|Com suporte<br /><br />Consulte Limitação 1, abaixo.|Com suporte<br /><br />Consulte Limitação 1, abaixo.|Com suporte<br /><br />Consulte Limitação 1, abaixo.|  
|Conta de Serviço de Rede (NT AUTHORITY\NetworkService)|Com suporte<br /><br />Consulte limitação 1, 3 e 4 abaixo.|Sem suporte|Sem suporte|  
|Conta de usuário local (não administrativa)|Com suporte<br /><br />Consulte Limitação 1, abaixo.|Sem suporte|Não aplicável|  
|Conta Sistema Local (NT AUTHORITY\System)|Com suporte<br /><br />Consulte Limitação 2, abaixo.|Sem suporte|Com suporte<br /><br />Consulte Limitação 2, abaixo.|  
|Conta do Serviço Local (NT AUTHORITY\LocalService)|Sem suporte|Sem suporte|Sem suporte|  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>Limitação 1: usar contas não administrativas para administração multisservidor  
A inscrição de servidores de destino para um servidor mestre pode falhar com a seguinte mensagem de erro: "Falha na operação de inscrição".  
  
Para resolver esse erro, reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](https://msdn.microsoft.com/32660a02-e5a1-411a-9e57-7066ca459df6).  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>Limitação 2: usar a conta Sistema Local para administração multisservidor  
Quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado com a conta Sistema Local, só haverá suporte para administração multisservidor se o servidor mestre e o servidor de destino residirem no mesmo computador. Se você usar essa configuração, será retornada a seguinte mensagem quando você inscrever servidores de destino para o servidor mestre:  
  
"Verifique se a conta de inicialização de agente de *<target_server_computer_name>* tem direitos para fazer logon como um servidor de destino".  
  
Você pode ignorar essa mensagem informativa. A operação de inscrição deve ser concluída com êxito. Para obter mais informações, veja [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>Limitação 3: usar a conta de Serviço de Rede, quando ela é um usuário do SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent poderá não conseguir iniciar se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com a conta de Serviço de Rede e esta tiver recebido acesso explicitamente para fazer logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Para resolver isso, reinicialize o computador em que está sendo executado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso só precisa ser feito uma vez.  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>Limitação 4: usar a conta de Serviço de Rede quando o SQL Server Reporting Services é executado no mesmo computador  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent poderá não conseguir iniciar se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com a conta do Serviço de Rede e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também estiver em execução no mesmo computador.  
  
Para resolver isso, reinicie o computador em que está sendo executado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, reinicialize os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Isso só precisa ser feito uma vez.  
  
## <a name="common-tasks"></a>Tarefas comuns  
**Para especificar a conta de inicialização do serviço do SQL Server Agent**  
  
-   [Definir a conta de inicialização de serviço para o SQL Server Agent &#40;SQL Server Configuration Manager&#41;](../../ssms/agent/set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
**Para especificar o perfil de email do SQL Server Agent**  
  
-   [Como: configurar o SQL Server Agent Mail para usar o Database Mail](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
> [!NOTE]  
> Use o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser iniciado quando o sistema operacional for iniciado.  
  
## <a name="see-also"></a>Consulte Também  
[Configurando as contas de serviço do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
[Gerenciamento de serviços usando o Gerenciador de Computador SQL](https://msdn.microsoft.com/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
