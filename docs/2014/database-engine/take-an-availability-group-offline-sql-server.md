---
title: Alterar grupo de disponibilidade offline
description: Etapas para definir seu grupo de disponibilidade Always On offline
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87dff347bd0aee1211093d9e3406a24670a80e7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75228166"
---
# <a name="take-an-availability-group-offline-sql-server"></a>Colocar um grupo de disponibilidade offline (SQL Server)
  Este tópico descreve como passar um grupo de disponibilidade AlwaysOn do estado ONLINE para o estado OFFLINE usando o [!INCLUDE[tsql](../includes/tsql-md.md)] no [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] e em versões posteriores. Não há perda de dados para bancos de dados de confirmação síncrona, pois, se alguma réplica de confirmação síncrona não é sincronizada, a operação OFFLINE gera um erro e deixa o grupo de disponibilidade ONLINE. Quando o grupo de disponibilidade permanece online, isso protege bancos de dados de confirmação síncrona não sincronizados contra possível perda de dados. Depois que um grupo de disponibilidade se torna offline, seus bancos de dados ficam indisponíveis para os clientes e você não pode recolocar o grupo de disponibilidade online. Portanto, coloque um grupo de disponibilidade offline somente para migrar os recursos do grupo de disponibilidade de um cluster WSFC para outro.  
  
 Durante uma migração entre clusters de [!INCLUDE[ssHADR](../includes/sshadr-md.md)], se algum aplicativo se conectar diretamente à réplica primária de um grupo de disponibilidade, o grupo de disponibilidade deverá ser colocado offline. A migração entre clusters de [!INCLUDE[ssHADR](../includes/sshadr-md.md)] dá suporte à atualização do sistema operacional com tempo de inatividade mínimo de grupos de disponibilidade. O cenário típico é usar a migração entre clusters de [!INCLUDE[ssHADR](../includes/sshadr-md.md)] para a atualização do sistema operacional para [!INCLUDE[win8](../includes/win8-md.md)] ou para o [!INCLUDE[win8srv](../includes/win8srv-md.md)]. Para obter mais informações, consulte [Migração entre clusters de grupos de disponibilidade AlwaysOn para atualização do sistema operacional](https://msdn.microsoft.com/library/jj873730.aspx).  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
> [!CAUTION]  
>  Use a opção OFFLINE apenas para uma migração entre clusters de recursos do grupo de disponibilidade.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   A instância de servidor na qual você insere o comando OFFLINE deve executar o [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] ou posterior (edição Enterprise ou superior).  
  
-   O grupo de disponibilidade deve estar online no momento.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
 Antes de você colocar o grupo de disponibilidade offline, exclua o ouvinte do grupo de disponibilidade ou os ouvintes. Para obter mais informações, veja [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para colocar um grupo de disponibilidade offline**  
  
1.  Conecte-se a uma instância de servidor que hospede uma réplica de disponibilidade do grupo de disponibilidade. Essa réplica pode ser a réplica primária ou uma réplica secundária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     em que *group_name* é o nome do grupo de disponibilidade.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir coloca o grupo de disponibilidade `AccountsAG` offline.  
  
```sql
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="follow-up-after-the-availability-group-goes-offline"></a><a name="FollowUp"></a>Acompanhamento: depois que o grupo de disponibilidade ficar offline  
  
-   **Registro em log da operação OFFLINE:**  a identidade do nó WSFC em que a operação OFFLINE foi iniciada é armazenada no log do cluster WSFC e no SQL ERRORLOG.  
  
-   **Se você não tiver excluído o ouvinte do grupo de disponibilidade antes de colocar o grupo offline:**  se você estiver migrando o grupo de disponibilidade para outro cluster WSFC, exclua o VNN e o VIP do ouvinte. É possível excluí-los usando o console do Gerenciamento de Cluster de Failover, o cmdlet [Remove-ClusterResource](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx) do PowerShell ou [cluster.exe](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx). Observe que cluster.exe foi preterido no Windows 8.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Alterar o contexto do cluster HADR da instância de servidor &#40;SQL Server&#41;](availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Artigos técnicos do SQL Server 2012](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](availability-groups/windows/always-on-availability-groups-sql-server.md)  
