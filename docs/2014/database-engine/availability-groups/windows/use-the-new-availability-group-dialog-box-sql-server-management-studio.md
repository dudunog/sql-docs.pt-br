---
title: Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 1b0a6421-fbd4-4bb4-87ca-657f4782c433
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee729f9f2bdd0044f2897a06e93f00b7b37ca785
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783135"
---
# <a name="use-the-new-availability-group-dialog-box-sql-server-management-studio"></a>Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio)
  Este tópico contém informações sobre como usar a caixa de diálogo **Novo Grupo de Disponibilidade** do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para criar um grupo de disponibilidade AlwaysOn em instâncias do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que são habilitadas para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Um *grupo de disponibilidade* define um conjunto de bancos de dados de usuários que realizará o failover como uma única unidade e um conjunto de parceiros de failover, conhecido como *réplicas de disponibilidade*, que oferece suporte a failover.  
  
> [!NOTE]  
>  Para obter uma introdução aos grupos de disponibilidade, consulte [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  

> [!NOTE]  
>   Para obter informações sobre modos alternativos de criar um grupo de disponibilidade, consulte [Tarefas relacionadas](#RelatedTasks), mais adiante neste tópico.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 É recomendável que você leia esta seção antes de tentar criar seu primeiro grupo de disponibilidade.  
  
###  <a name="prerequisites"></a><a name="PrerequisitesRestrictions"></a> Pré-requisitos  
  
-   Antes de criar um grupo de disponibilidade, verifique se as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam réplicas de disponibilidade residem em um nó diferente do WSFC (Windows Server Failover Clustering), dentro do mesmo cluster de failover do WSFC. Também verifique se cada instância de servidor está habilitada para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] atende a todos os outros pré-requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter mais informações, é altamente recomendável que você leia [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Antes de você criar um grupo de disponibilidade, verifique se toda instância de servidor que hospedará uma réplica de disponibilidade tem um ponto de extremidade de espelhamento de banco de dados funcionando perfeitamente. Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
-   Para usar a caixa de diálogo **Novo Grupo de Disponibilidade** , você precisa saber os nomes das instâncias de servidor que hospedarão réplicas de disponibilidade. Além disso, você precisa saber os nomes dos bancos de dados que pretende adicionar ao seu novo grupo de disponibilidade e verificar se eles atendem aos pré-requisitos de banco de dados de disponibilidade e às restrições descritas em [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md). Se você inserir valores inválidos, o novo grupo de disponibilidade não funcionará.  
  
###  <a name="limitations"></a><a name="Limitations"></a> Limitações  
 A caixa de diálogo **Novo Grupo de Disponibilidade** não permite:  
  
-   Criar um ouvinte de grupo de disponibilidade.  
  
-   Unir réplicas secundárias ao grupo de disponibilidade.  
  
-   Executar a sincronização de dados inicial.  
  
 Para obter informações sobre essas tarefas de configuração, consulte [Acompanhamento: depois de criar um grupo de disponibilidade](#FollowUp), mais adiante neste tópico.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-the-new-availability-group-dialog-box-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando a caixa de diálogo novo grupo de disponibilidade (SQL Server Management Studio)  
 **Para criar um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e clique no nome do servidor.  
  
2.  Expanda o nó **Alta Disponibilidade AlwaysOn** .  
  
3.  Clique com o botão direito do mouse no nó **Grupos de Disponibilidade** e selecione o comando **Novo Grupo de Disponibilidade** .  
  
4.  Esse comando abre a caixa de diálogo **Novo Grupo de Disponibilidade** .  
  
5.  Na página **Geral** , use o campo **Nome do grupo de disponibilidade** para digitar o nome do novo grupo de disponibilidade. Esse nome deve ser um identificador válido do SQL Server e exclusivo em todos os grupos de disponibilidade no cluster WSFC. O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  
  
6.  Na grade **Bancos de Dados de Disponibilidade** , clique em **Adicionar** e digite o nome de um banco de dados local que você deseja incluir nesse grupo de disponibilidade. Repita isso para todos os bancos de dados a serem adicionados. Quando você clicar em **OK**, a caixa de diálogo verificará se seu banco de dados especificado atende aos pré-requisitos para pertencer a um grupo de disponibilidade. Para obter informações sobre esses pré-requisitos, consulte [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
7.  Na grade **Bancos de dados de Disponibilidade** , clique em **Adicionar** e digite o nome de uma instância de servidor para hospedar uma réplica secundária. A caixa de diálogo não tentará se conectar a essas instâncias. Se você especificar um nome de servidor incorreto, uma réplica secundária será adicionada, mas você não poderá se conectar a ela.  
  
    > [!TIP]  
    >  Se você tiver adicionado uma réplica e não conseguir conectar-se à instância de servidor host, poderá remover a réplica e adicionar uma nova. Para obter mais informações, veja [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md) e [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
8.  No painel **Selecionar uma página** da caixa de diálogo, clique em **Preferências de Backup**. Em seguida, na página **Preferências de Backup** , especifique onde os backups devem ocorrer com base na função de réplica e atribua prioridades de backup a cada instância de servidor que hospedará uma réplica de disponibilidade para esse grupo de disponibilidade. Para obter mais informações consulte [Propriedades de grupo de disponibilidade/Novo grupo de disponibilidade &#40;página Preferências de Backup&#41;](availability-group-properties-new-availability-group-backup-preferences-page.md).  
  
9. Para criar o grupo de disponibilidade, clique em **OK**. Isso faz com que a caixa de diálogo verifique se os bancos de dados especificados atendem aos pré-requisitos.  
  
     Para sair da caixa de diálogo sem criar o grupo de disponibilidade, clique em **Cancelar**.  
  
##  <a name="follow-up-after-using-the-new-availability-group-dialog-box-to-create-an-availability-group"></a><a name="FollowUp"></a>Acompanhamento: depois de usar a caixa de diálogo novo grupo de disponibilidade para criar um grupo de disponibilidade  
  
-   Você precisa conectar-se a cada instância de servidor, uma por vez, que está hospedando uma réplica secundária para o grupo de disponibilidade e concluir as seguintes etapas:  
  
    1.  Una a réplica secundária ao grupo de disponibilidade. Para obter mais informações, veja [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
    2.  Restaure os backups atuais de cada banco de dados primário e seu log de transações (usando RESTORE WITH NORECOVERY). Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
    3.  Una imediatamente cada banco de dados secundário recém-preparado ao grupo de disponibilidade. Para obter mais informações, consulte [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
-   Recomendamos que você crie um ouvinte de grupo de disponibilidade para o novo grupo de disponibilidade. Isso exige que você esteja conectado à instância do servidor que hospeda a réplica primária atual. Para obter mais informações, consulte [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar um grupo de disponibilidade e propriedades de réplica**  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar a política de failover flexível para controlar condições de failover automático (grupos de disponibilidade AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para concluir a configuração do grupo de disponibilidade**  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneiras alternativas de criar um grupo de disponibilidade**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **Para habilitar Grupos de Disponibilidade AlwaysOn**  
  
-   [Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para Grupos de Disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para solucionar problemas de configuração de grupos de disponibilidade AlwaysOn**  
  
-   [Solução de problemas de configuração de Grupos de Disponibilidade AlwaysOn (SQL Server) excluída](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solucionar problemas de uma operação de adição de arquivo com falha &#40;Grupos de Disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Ouvintes de grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
