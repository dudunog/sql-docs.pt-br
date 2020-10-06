---
title: Pré-requisitos para converter o envio de logs para grupos de disponibilidade
description: Uma descrição dos pré-requisitos necessários para converter o envio de logs em um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dd1fe3943fe3e5c36dc60df147a2c2ec77a4dac2
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670129"
---
# <a name="prerequisites-to-convert-log-shipping-to-always-on-availability-groups"></a>Pré-requisitos para converter o envio de logs para grupos de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Esse tópico descreve os pré-requisitos para converter um banco de dados primário para envio de logs junto com um ou mais de seus bancos de dados secundários para um banco de dados primário AlwaysOn e bancos de dados secundários.  
  
> [!NOTE]  
>  Você pode configurar qualquer banco de dados primário ou secundário (possivelmente legível) em um grupo de disponibilidade como um banco de dados primário de envio de logs.  
  
  
##  <a name="availability-group-prerequisites"></a><a name="AGPrereqsRealAddress"></a> Pré-requisitos do grupo de disponibilidade  
 Para permitir que trabalhos de backup sejam executados na réplica primária do grupo de disponibilidade, use as seguintes configurações de backup dos Grupos de Disponibilidade AlwaysOn:  
  
|Propriedade|Configuração|  
|--------------|-------------|  
|A preferência de backup automatizada do grupo de disponibilidade|Apenas na réplica primária|  
|Prioridade de backup da réplica primária.|>0|  
  
 **Para obter mais informações, consulte:**  
  
 [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="log-shipping-prerequisites"></a><a name="LogShipPrereqs"></a> Pré-requisitos para envio de logs  
  
-   O banco de dados primário para envio de logs deve residir na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária inicial/atual do grupo de disponibilidade.  
  
-   Para determinado banco de dados secundário para envio de log ser convertido em um banco de dados secundário AlwaysOn, ele deverá:  
  
    -   Usar o mesmo nome que o banco de dados primário.  
  
    -   Residir em uma instância de servidor que hospeda uma réplica secundária para o grupo de disponibilidade.  
  
 Quando o trabalho de backup estiver sendo executado no banco de dados primário, desabilite o trabalho de backup e, assim que o trabalho de restauração tiver sido executado em um determinado banco de dados secundário, desabilite o trabalho de restauração.  
  
 Depois que você criar todos os bancos de dados secundários para o grupo de disponibilidade, se você desejar executar backups em réplicas secundárias, precisará reconfigurar a preferência de backup automatizada do grupo de disponibilidade.  
  
 **Para obter mais informações, consulte:**  
  
 [Convertendo uma configuração de envio de logs para grupo de disponibilidade](/archive/blogs/sqlalwayson/converting-a-logshipping-configuration-to-availability-group) (um blog do SQL Server)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Envio de logs**  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **Grupos de disponibilidade AlwaysOn**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Convertendo uma configuração para envio de logs para Grupo de Disponibilidade](/archive/blogs/sqlalwayson/converting-a-logshipping-configuration-to-availability-group)  
  
     [Adicione um banco de dados primário de envio de logs e bancos de dados secundários a um grupo de disponibilidade existente](/archive/blogs/sqlalwayson/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](/archive/blogs/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](/archive/blogs/psssql/)  
  
-   **Whitepapers:**  
  
     [Guia de migração: Migrando para grupos de disponibilidade AlwaysOn de implantações anteriores que combinam espelhamento de banco de dados e envio de logs](/previous-versions/sql/sql-server-2012/jj635217(v=msdn.10))  
  
     [White papers da Microsoft para SQL Server 2012](https://social.technet.microsoft.com/wiki/contents/articles/13146.white-paper-gallery-for-sql-server.aspx#[Category]SQLServer2012)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
