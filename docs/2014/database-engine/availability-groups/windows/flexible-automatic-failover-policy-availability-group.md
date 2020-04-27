---
title: Política de failover flexível para failover automático de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63c9f56894ede1002b358c624ab763935fd42fc1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62789888"
---
# <a name="flexible-failover-policy-for-automatic-failover-of-an-availability-group-sql-server"></a>Política de failover flexível para failover automático de um grupo de disponibilidade (SQL Server)
  Uma política de failover flexível fornece controle granular sobre as condições que causam [failover automático](failover-and-failover-modes-always-on-availability-groups.md) para um grupo de disponibilidade. Ao alterar as condições de falha que disparam um failover automático e a frequência de verificações de integridade, você pode aumentar ou diminuir a probabilidade de um failover automático para oferecer suporte ao seu SLA para alta disponibilidade.  
  
 A política de failover flexível de um grupo de disponibilidade é definida por seu nível da condição de falha e pelo limite de tempo limite da verificação de integridade. Ao detectar que um grupo de disponibilidade excedeu seu nível de condição de falha ou seu limite de tempo limite da verificação de integridade, a DLL de recurso do grupo de disponibilidade responde ao cluster WSFC (Windows Server Failover Clustering). O cluster WSFC inicia um failover automático para a réplica secundária.  
  
> [!IMPORTANT]  
>  Se um grupo de disponibilidade exceder seu limite de falha do WSFC, o cluster do WSFC não tentará um failover automático para o grupo de disponibilidade. Além disso, o grupo de recursos do WSFC do grupo de disponibilidade permanece em um estado com falha até o administrador de cluster manualmente colocar online o grupo de recursos com falha ou o administrador de banco de dados executar um failover manual do grupo de disponibilidade. O *limite de falha do WSFC* é definido como o número máximo de falhas com suporte para o grupo de disponibilidade durante um determinado período de tempo. O período padrão é de seis horas e o valor padrão para o número máximo de falhas durante este período é *n*-1, em que *n* é o número de nós do WSFC. Para alterar os valores do limite de failover para um determinado grupo de disponibilidade, use o Console de Gerenciador de Failover WSFC.  
  
  
  
##  <a name="health-check-timeout-threshold"></a><a name="HCtimeout"></a> Limite do tempo limite da verificação de integridade  
 A DLL de recurso do WSFC do grupo de disponibilidade executa uma *verificação de integridade* da réplica primária, chamando o procedimento armazenado [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) na instância do SQL Server que hospeda a réplica primária. **sp_server_diagnostics** retorna resultados em um intervalo 1/3 em relação ao limite do tempo limite da verificação de integridade para o grupo de disponibilidade. O limite do tempo limite da verificação de integridade padrão é de 30 segundos, levando **sp_server_diagnostics** a retornar em um intervalo de 10 segundos. Se **sp_server_diagnostics** for lento ou não estiver retornando informações, a DLL de recurso aguardará o intervalo completo do limite de tempo limite da verificação de integridade antes de determinar que a réplica primária não está respondendo. Se a réplica primária não estiver respondendo, um failover automático será iniciado, se tiver suporte no momento.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** não realiza verificações de integridade no nível de banco de dados.  
  
##  <a name="failure-condition-level"></a><a name="FClevel"></a> Nível da condição de falha  
 O nível da condição de falha do grupo de disponibilidade determina se os dados de diagnóstico e as informações de integridade retornadas por **sp_server_diagnostics** garantem um failover automático. O *nível de condição de falha* especifica as condições de falha que disparam um failover automático. Há cinco níveis da condição de falha que variam do menos restritivo (nível 1) até o mais restritivo (nível 5). Um nível específico abrange todos os níveis menos restritivos. Portanto, o nível mais rígido, cinco, inclui os quatro níveis de condições menos restritivos e assim por diante.  
  
> [!IMPORTANT]  
>  Bancos de dados danificados e bancos de dados suspeitos não são detectados por nenhum nível de condição de falha. Portanto, um banco de dados que esteja danificado ou suspeito (seja devido a um problema de hardware, corrupção de dados ou outro problema) nunca dispara um failover automático.  
  
 A tabela a seguir descreve as condições de falha que correspondem a cada nível.  
  
|Nível|Condição de falha|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Valor de PowerShell|  
|-----------|-----------------------|------------------------------|----------------------|  
|Um|Em servidor inativo. Este é o nível menos restritivo. Especifica que um failover automático é iniciado quando uma destas condições ocorre:<br /><br /> O serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está inativo.<br /><br /> A concessão do grupo de disponibilidade para conexão com o cluster WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, consulte [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx).|1|`OnServerDown`|  
|Dois|Em servidor sem resposta. Especifica que um failover automático é iniciado quando uma destas condições ocorre:<br /><br /> A instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não se conecta ao cluster e o limite de tempo limite especificado pelo usuário do grupo de disponibilidade é excedido.<br /><br /> A réplica de disponibilidade está em estado de falha.|2|`OnServerUnresponsive`|  
|Três|Em erros críticos do servidor. Especifica que um failover automático é iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como spinlocks órfãos, violações do acesso de gravação graves ou muito despejo. Este é o nível padrão.|3|`OnCriticalServerError`|  
|Quatro|Em erros moderados do servidor. Especifica que um failover automático é iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|4|`OnModerateServerError`|  
|Cinco|Em qualquer condição de falha qualificada. Este é o nível mais restritivo. Especifica que um failover automático é iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> Esgotamento dos threads de trabalho do SQL Engine.<br /><br /> Detecção de um deadlock insolúvel.|5|`OnAnyQualifiedFailureConditions`|  
  
> [!NOTE]  
>  A falta de resposta de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para solicitações do cliente é irrelevante para grupos de disponibilidade.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar o failover automático**  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md) (o failover automático exige o modo de disponibilidade de confirmação síncrona)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar a política de failover flexível para controlar condições de failover automático (grupos de disponibilidade AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidade (Grupos de Disponibilidade AlwaysOn)](availability-modes-always-on-availability-groups.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [O Windows Server failover clustering &#40;&#41; WSFC com SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Política de failover para instâncias de cluster de failover](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
  
  
