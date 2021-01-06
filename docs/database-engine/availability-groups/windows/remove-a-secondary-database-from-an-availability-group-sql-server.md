---
title: Remover um banco de dados secundário de um grupo de disponibilidade
description: Etapas para remoção de um banco de dados secundário de um grupo de disponibilidade Always On usando o T-SQL (Transact-SQL), o PowerShell ou o SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.unjoindb.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], databases
ms.assetid: 4e51a570-58d7-4f01-9390-4198f3602576
author: cawrites
ms.author: chadam
ms.openlocfilehash: 03d286ae75d9bfeeb1304633b4ddf1f790979fdf
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642462"
---
# <a name="remove-a-secondary-database-from-an-availability-group-sql-server"></a>Remover um banco de dados primário de um grupo de disponibilidade (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como remover um banco de dados secundário de um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
   
  
##  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Esta tarefa tem suporte apenas em réplicas secundárias. Você deve estar conectado à instância do servidor que hospeda a réplica secundária da qual o banco de dados deve ser removido.  
  
 
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para remover um banco de dados secundário de um grupo de disponibilidade**  
  
1.  Em Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica secundária da qual você deseja remover um ou mais bancos de dados secundários e expanda a árvore de servidor.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Selecione o grupo de disponibilidade e expanda o nó **Bancos de Dados de Disponibilidade** .  
  
4.  Essa etapa depende de se você deseja remover vários grupos de bancos de dados ou apenas um banco de dados, da seguinte maneira:  
  
    -   Para remover vários bancos de dados, use o painel **Detalhes do Pesquisador de Objetos** para exibir e selecionar todos os bancos de dados que você deseja remover. Para obter mais informações, veja [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para remover um único banco de dados, selecione-o no painel **Pesquisador de Objetos** ou no painel **Detalhes do Pesquisador de Objetos** .  
  
5.  Clique com o botão direito do mouse no banco de dados ou bancos de dados selecionados e selecione **Remover Banco de Dados Secundário** no menu de comando.  
  
6.  Na caixa de diálogo **Remover Banco de Dados do Grupo de Disponibilidade** , para remover todos os bancos de dados listados, clique em **OK**. Se você não desejar remover todos os bancos de dados listados, clique em **Cancelar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para remover um banco de dados secundário de um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica secundária.  
  
2.  Use a [cláusula SET HADR da instrução ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) , da seguinte maneira:  
  
     ALTER DATABASE *database_name* SET HADR OFF  
  
     em que *database_name* é o nome de um banco de dados secundário a ser removido do grupo de disponibilidade ao qual pertence.  
  
     O exemplo a seguir remove o banco de dados secundário local *MyDb2* de seu grupo de disponibilidade.  
  
    ```  
    ALTER DATABASE MyDb2 SET HADR OFF;  
    GO  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para remover um banco de dados secundário de um grupo de disponibilidade**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica secundária.  
  
2.  Use o cmdlet **Remove-SqlAvailabilityDatabase** , especificando o nome do banco de dados de disponibilidade a ser removido do grupo de disponibilidade. Quando você está conectado a uma instância do servidor que hospeda uma réplica secundária, apenas o banco de dados secundário local é removido do grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir remove o banco de dados secundário `MyDb8` da réplica secundária hospedada pela instância de servidor denominada `SecondaryComputer\Instance`. A sincronização de dados para os bancos de dados secundários removidos é encerrada. Este comando não afeta o banco de dados primário ou nenhum outro banco de dados secundário.  
  
    ```  
    Remove-SqlAvailabilityDatabase `  
    -Path SQLSERVER:\Sql\SecondaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb8  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-after-removing-a-secondary-database-from-an-availability-group"></a><a name="FollowUp"></a> Acompanhamento: depois de remover um banco de dados secundário de um grupo de disponibilidade  
 Quando um banco de dados secundário é removido, ele não é mais unido ao grupo de disponibilidade, e todas as informações sobre o banco de dados secundário removido são descartadas pelo grupo de disponibilidade. O banco de dados secundário removido é colocado no estado RESTORING.  
  
> [!TIP]  
>  Pouco tempo depois de remover um banco de dados secundário, você poderá reiniciar a sincronização de dados AlwaysOn no banco de dados reassociando-o ao grupo de disponibilidade. Para obter mais informações, consulte [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
 Neste ponto, há maneiras alternativas de lidar com um banco de dados secundário removido:  
  
-   Se você não precisar mais do banco de dados secundário, você poderá removê-lo.  
  
     Para obter mais informações, consulte [DROP DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-transact-sql.md) ou [Excluir um banco de dados](../../../relational-databases/databases/delete-a-database.md).  
  
-   Se desejar acessar um banco de dados secundário depois que ele foi removido do grupo de disponibilidade, você poderá recuperá-lo. No entanto, se você recuperar um banco de dados secundário removido, dois bancos de dados independentes divergentes com o mesmo nome estarão online. Você deve ter certeza de que os clientes podem acessar apenas o banco de dados primário atual.  
  
     Para obter mais informações, veja [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
