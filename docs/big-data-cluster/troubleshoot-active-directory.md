---
title: Solucionar problemas do escopo do grupo de domínio do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Solucionar problemas de implantação de um cluster de Big Data do SQL Server em um domínio do Active Directory.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 302731f3f0c37f60c4944b7df44d02b2cfc64a8b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772881"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-integration"></a>Solucionar problemas de integração do Active Directory com o cluster de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo explica como solucionar problemas de implantação de um Cluster de Big Data do SQL Server no modo Active Directory.

## <a name="symptom"></a>Sintoma

Você começou a implantar o BDC com o modo AD, mas a implantação está paralisada e não está avançando.

O exemplo a seguir mostra os resultados da implantação em um shell com o bash.

```
The privacy statement can be viewed at:
https://go.microsoft.com/fwlink/?LinkId=853010
 
The license terms for SQL Server Big Data Cluster can be viewed at:
Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292
Standard: https://go.microsoft.com/fwlink/?linkid=2104294
Developer: https://go.microsoft.com/fwlink/?linkid=2104079
 
Cluster deployment documentation can be viewed at:
https://aka.ms/bdc-deploy
 
NOTE: Cluster creation can take a significant amount of time depending on
configuration, network speed, and the number of nodes in the cluster.
 
Starting cluster deployment.
Cluster controller endpoint is available at bdc-control.contoso.com:30080, 193.168.5.14:30080.
Waiting for control plane to be ready after 5 minutes.
Waiting for control plane to be ready after 10 minutes.
Waiting for control plane to be ready after 15 minutes.
Waiting for control plane to be ready after 20 minutes.
Waiting for control plane to be ready after 25 minutes.
```

Verifique os pods implantados atualmente.

```bash
kubectl get pods -n mssql-cluster
```

A lista a seguir mostra apenas os pods que pertencem ao controlador e que foram implantados. Nenhum pod de computação, dados ou pool de armazenamento está sendo criado.

```
NAME              READY   STATUS    RESTARTS   AGE
appproxy-6q4rm    2/2     Running   0          32m
compute-0-0       3/3     Running   0          32m
control-n8jqh     3/3     Running   0          35m
controldb-0       2/2     Running   0          35m
controlwd-fgpj8   1/1     Running   0          34m
data-0-0          3/3     Running   0          32m
data-0-1          3/3     Running   0          32m
dns-fjp7n         2/2     Running   0          34m
gateway-0         2/2     Running   0          32m
logsdb-0          1/1     Running   0          34m
logsui-d26c5      1/1     Running   0          34m
master-0          3/4     Running   0          32m
master-1          3/4     Running   0          32m
master-2          3/4     Running   0          32m
metricsdb-0       1/1     Running   0          34m
metricsdc-c2kbh   1/1     Running   0          34m
metricsdc-lmqzx   1/1     Running   0          34m
metricsdc-r6499   1/1     Running   0          34m
metricsdc-tj99w   1/1     Running   0          34m
metricsui-dg8rz   1/1     Running   0          34m
mgmtproxy-dvzpc   2/2     Running   0          34m
nmnode-0-0        2/2     Running   0          32m
nmnode-0-1        2/2     Running   0          32m
operator-27gt9    1/1     Running   0          32m
sparkhead-0       4/4     Running   0          31m
sparkhead-1       4/4     Running   0          31m
storage-0-0       4/4     Running   0          31m
storage-0-1       4/4     Running   0          31m
storage-0-2       4/4     Running   0          31m
zookeeper-0       2/2     Running   0          32m
zookeeper-1       2/2     Running   0          32m
zookeeper-2       2/2     Running   0          32m
```

### <a name="check-logs"></a>Verificar os logs

Para identificar por que a implantação é encerrada sem criar pods de computação, dados ou armazenamento, verifique os seguintes logs: 

- Verifique `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`). Procure a seguinte entrada:

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- Verifique `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

## <a name="cause"></a>Causa

No exemplo acima, a implantação não cria um logon para o usuário de domínio porque o grupo de domínio está no escopo como domínio local. Use grupos com escopo global ou universal. [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo Active Directory](deploy-active-directory.md) explica os requisitos de escopo do grupo do AD.

## <a name="verify"></a>Verificar

Verifique o escopo do grupo de domínio (<`domain-group`>). Use [get-adgroup](/powershell/module/addsadministration/get-adgroup/).

Se o escopo do grupo `<domain-group>` for local do domínio (`DomainLocal`), a implantação falhará. 

O script do PowerShell a seguir verifica o escopo de dois grupos do AD chamados `bdcadmins` e `bdcusers`. Substitua os nomes pelos nomes dos grupos. 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="resolution"></a>Resolução

Para resolver o problema, crie os grupos do AD com escopo universal ou global e execute a implantação novamente.

