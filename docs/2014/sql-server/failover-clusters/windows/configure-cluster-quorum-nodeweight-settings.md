---
title: Definir configurações de NodeWeight de quórum de cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfc31fa968952db56a64f93b180c2b88ec685725
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797610"
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>Definir configurações de NodeWeight de quorum de cluster
  Este tópico descreve como definir configurações de NodeWeight para um nó de membro em um cluster WSFC (Windows Server Failover Clustering). As configurações de NodeWeight são usadas durante a votação de quorum para dar suporte à recuperação de desastre e a cenários com várias sub-redes para instâncias de cluster de failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Antes de iniciar:**  [Pré-requisitos](#Prerequisites), [Segurança](#Security)  
  
-   **Para exibir as configurações de NodeWeight de quorum usando:** [Usando o PowerShell](#PowerShellProcedure), [Usando Cluster.exe](#CommandPromptProcedure)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="before-you-start"></a><a name="BeforeYouBegin"></a> Antes de iniciar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Esse recurso somente tem suporte no [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] ou em versões posteriores.  
  
> [!IMPORTANT]  
>  Para usar configurações de NodeWeight, é necessário aplicar o seguinte hotfix para todos os servidores no cluster WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): Há um hotfix disponível para permitir que você configure um nó de cluster que não tenha votos de quorum em [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e em [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Se esse hotfix não for instalado, os exemplos neste tópico retornarão valores vazios ou NULL para NodeWeight.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 O usuário deve ser uma conta de domínio que seja membro do grupo Administradores local em cada nó do cluster WSFC.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o Powershell  
  
### <a name="to-configure-nodeweight-settings"></a>Para definir configurações de NodeWeight
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo `FailoverClusters` para habilitar commandlets de cluster.  
  
3.  Use o objeto `Get-ClusterNode` para definir a propriedade `NodeWeight` para cada nó no cluster.  
  
4.  Gere as propriedades de nó de cluster em um formato legível.  
  
 O exemplo a seguir altera a configuração de NodeWeight para remover o voto de quorum do nó "AlwaysOnSrv1" e gera as configurações de todos os nós no cluster.
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv1"  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="using-clusterexe"></a><a name="CommandPromptProcedure"></a> Usando Cluster.exe  
  
> [!NOTE]  
>  O utilitário cluster.exe foi preterido na versão [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Use o PowerShell com Clustering de Failover para desenvolvimento futuro.  O utilitário cluster.exe será removido na próxima versão do Windows Server. Para obter mais informações, consulte [Mapeando comandos cluster.exe para cmdlets Windows PowerShell para clusters de failover](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
### <a name="to-configure-nodeweight-settings"></a>Para definir configurações de NodeWeight
  
1.  Inicie um Prompt de Comando elevado via **Executar como Administrador**.  
  
2.  Use **cluster.exe** para definir valores de `NodeWeight` .  

 O exemplo a seguir altera o valor de NodeWeight para remover o voto de quorum do nó "AlwaysOnSrv1" no cluster "Cluster001".  
  
```cmd
cluster.exe Cluster001 node AlwaysOnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Exibir eventos e logs de um cluster de failover](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cluster de failover Get-ClusterLog do cmdlet](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Os modos de quorum WSFC e a configuração de votação &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Exibir configurações de NodeWeight de quorum de cluster](view-cluster-quorum-nodeweight-settings.md)   
 [Cmdlets de cluster de failover no Windows PowerShell listados por foco de tarefa](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
