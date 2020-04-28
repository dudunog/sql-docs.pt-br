---
title: Retomar um banco de dados de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5e6a5792c7e18013dba5cc4c0963dc6d045410f0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782917"
---
# <a name="resume-an-availability-database-sql-server"></a>Retomar um banco de dados de disponibilidade (SQL Server)
  Você pode retomar um banco de dados de disponibilidade suspenso no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. A retomada de um banco de dados suspenso coloca o banco de dados no estado SYNCHRONIZING. A retomada do banco de dados primário também retoma todos os bancos de dados secundários que foram suspensos devido à suspensão do banco de dados primário. Se um banco de dados secundário foi suspenso localmente, na instância de servidor que hospeda a réplica secundária, o banco de dados secundário deverá ser retomado localmente. Quando um determinado banco de dados secundário e o banco de dados primário correspondente estiverem no estado SYNCHRONIZING, a sincronização de dados é retomada no banco de dados secundário.  
  
> [!NOTE]  
>  Suspender e retomar um banco de dados secundário AlwaysOn não afetam diretamente a disponibilidade do banco de dados primário. Porém, suspender um banco de dados secundário pode afetar os recursos de redundância e failover para o banco de dados primário, até que o banco de dados secundário suspenso seja retomado. Isto está em contraste com o espelhamento de banco de dados, onde o estado de espelhamento é suspenso no banco de dados espelho e no banco de dados principal até que o espelhamento seja retomado. Suspender um banco de dados secundário AlwaysOn suspende o movimento de dados em todos os bancos de dados secundários correspondentes, e os recursos de failover e a redundância são eliminados para esse banco de dados até que o banco de dados primário seja retomado.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para retomar um banco de dados secundário usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 O comando RESUME retorna assim que é aceito pela réplica que hospeda o banco de dados de destino, mas, na verdade, a retomada do banco de dados ocorre de forma assíncrona.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância de servidor que hospeda o banco de dados a ser retomado.  
  
-   O grupo de disponibilidade deve estar online.  
  
-   O banco de dados primário deve estar online e disponível.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para retomar um banco de dados secundário**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica de disponibilidade na qual você deseja retomar o banco de dados e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Expanda o grupo de disponibilidade.  
  
4.  Expanda o nó **Bancos de dados de Disponibilidade** , clique com o botão direito do mouse no banco de dados e clique em **Retomar a Movimentação de Dados**.  
  
5.  Na caixa de diálogo **Retomar a Movimentação de Dados** , clique em **OK**.  
  
> [!NOTE]  
>  Para retomar bancos de dados adicionais neste local de réplica, repita as etapas 4 e 5 para cada banco de dados.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para retomar um banco de dados secundário que foi suspenso localmente**  
  
1.  Conecte-se à instância do servidor que hospeda a réplica secundária, cujo banco de dados você deseja retomar.  
  
2.  Retome o banco de dados secundário usando a seguinte instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr):  
  
     ALTER DATABASE *database_name* Set HADR resume  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  

### <a name="to-resume-a-secondary-database"></a>Para retomar um banco de dados secundário
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica cujo banco de dados você deseja retomar. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
2.  Use o cmdlet **Resume-SqlAvailabilityDatabase** para retomar o grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir retoma a sincronização dos dados para o banco de dados de disponibilidade `MyDb3` no grupo de disponibilidade `MyAg`.  
  
    ```powershell
    Resume-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Suspender um banco de dados de disponibilidade &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
