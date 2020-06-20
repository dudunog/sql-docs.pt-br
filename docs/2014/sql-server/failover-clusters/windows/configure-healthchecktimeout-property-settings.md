---
title: Definir configurações da propriedade HealthCheckTimeout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a38cd6e9e4718a2f1c136e5412cde340e92f14c1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062506"
---
# <a name="configure-healthchecktimeout-property-settings"></a>Definir configurações da propriedade HealthCheckTimeout
  A configuração HealthCheckTimeout é usada para especificar o tempo, em milissegundos, que a DLL de recursos do SQL Server deve aguardar por informações retornadas pelo procedimento armazenado [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) antes de relatar a FCI (Instância de Cluster de Failover) AlwaysOn como sem resposta. As alterações feitas nas configurações de tempo limite entram em vigor imediatamente e não requerem uma reinicialização do recurso do SQL Server.  
  
-   **Antes de começar:**  [Limitações e restrições](#Limits), [Segurança](#Security)  
  
-   **Para definir a configuração HeathCheckTimeout usando:**  [PowerShell](#PowerShellProcedure), [Gerenciador de Cluster de Failover](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Limits"></a> Limitações e restrições  
 O valor padrão dessa propriedade é 60.000 milissegundos (60 segundos). O valor mínimo é 15.000 milissegundos (15 segundos).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer as permissões ALTER SETTINGS e VIEW SERVER STATE.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
  
### <a name="to-configure-healthchecktimeout-settings"></a>Para configurar HealthCheckTimeout  
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo `FailoverClusters` para habilitar cmdlets de cluster.  
  
3.  Use o `Get-ClusterResource` cmdlet para localizar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recurso e, em seguida, use o `Set-ClusterParameter` cmdlet para definir a propriedade **HealthCheckTimeout** para a instância de cluster de failover.  
  
> [!TIP]  
>  Sempre que você abrir uma nova janela do PowerShell, deverá importar o módulo `FailoverClusters`.  

 O exemplo a seguir altera a configuração HealthCheckTimeout no recurso " [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] " do`SQL Server (INST1)`para 60.000 milissegundos.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
```  
  
### <a name="related-content-powershell"></a>Conteúdo relacionado (PowerShell)  
  
-   [Clustering e alta disponibilidade](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (Blog da equipe de Clustering de Failover e Balanceamento de Carga de Rede)  
  
-   [Guia de Introdução ao Windows PowerShell em um cluster de failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de cluster e cmdlets equivalentes no Windows PowerShell](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> Usando o snap-in Gerenciador de Cluster de Failover  
 **Para definir a configuração HealthCheckTimeout**  
  
1.  Abra o snap-in Gerenciador de Cluster de Failover.  
  
2.  Expanda **Serviços e Aplicativos** e selecione a FCI.  
  
3.  Clique com o botão direito do mouse em **Recurso de SQL Server** em **Outros Recursos** e selecione **Propriedades** no menu de atalho. A caixa de diálogo **Propriedades** do recurso do SQL Server é aberta.  
  
4.  Selecione a guia **Propriedades** , insira o valor desejado para a propriedade **HealthCheckTimeout** e clique em **OK** para aplicar a alteração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Usando a instrução [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , você pode especificar o valor da propriedade HealthCheckTimeOut.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir define a opção HealthCheckTimeout como 15.000 milissegundos (15 segundos).  
  
```sql
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Política de failover para instâncias de cluster de failover](failover-policy-for-failover-cluster-instances.md)  
