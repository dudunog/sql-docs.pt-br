---
title: Implantar o grupo de disponibilidade com o HPE Serviceguard – SQL Server em Linux
description: Usar o HPE Serviceguard como o gerenciador de cluster para obter alta disponibilidade com um grupo de disponibilidade no SQL Server em Linux
ms.date: 01/15/2021
ms.prod: sql
ms.technology: linux
ms.topic: tutorial
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.openlocfilehash: 3956c0470ac9f4b3ac2f2a35ed057015db6ea0e0
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534857"
---
# <a name="tutorial---setup-a-three-node-always-on-availability-group-with-hpe-serviceguard-for-linux"></a>Tutorial – Configurar um grupo de disponibilidade Always On de três nós com o HPE Serviceguard para Linux 

Esse tutorial explica como configurar um grupo de disponibilidade do SQL Server Always On com o HPE Serviceguard para Linux em execução em VMs (máquinas virtuais) locais.

Confira [Clusters do HPE Serviceguard](https://h20195.www2.hpe.com/v2/GetPDF.aspx/c04154488.pdf) para obter uma visão geral dos clusters do HPE Serviceguard.

> [!NOTE]
> A Microsoft dá suporte à movimentação de dados, ao grupo de disponibilidade e aos componentes do SQL Server. Entre em contato com a HPE para obter suporte relacionado à documentação sobre gerenciamento de cluster e de quorum do HPE Serviceguard.

Este tutorial é composto pelas seguintes etapas:

> [!div class="checklist"]
> * Instalar SQL Server em todas as três VMs que serão parte do grupo de disponibilidade
> * Instalar o HPE Serviceguard nas VMs
> * Criar o cluster do HPE Serviceguard
> * Criar o grupo de disponibilidade e adicionar um banco de dados de exemplo ao grupo de disponibilidade
> * Implantar a carga de trabalho do SQL Server no grupo de disponibilidade por meio do gerenciador de cluster do Serviceguard
> * Realizar um failover automático e ingressar o nó de volta no cluster

## <a name="prerequisites"></a>Pré-requisitos

* Três VMs em um ambiente local, executando o HPE Serviceguard em uma distribuição do Linux compatível.

   Para obter um exemplo de uma distribuição compatível, confira [HPE Serviceguard para Linux](https://h20195.www2.hpe.com/v2/gethtml.aspx?docname=c04154488).

   Verifique junto à HPE como obter informações sobre o suporte para ambientes de nuvem pública.

   As instruções no tutorial são validadas junto ao HPE Serviceguard para Linux. Uma edição de avaliação está disponível para download com a [HPE](https://www.hpe.com/us/en/resources/servers/serviceguard-linux-trial.html).

* Arquivos de banco de dados do SQL Server na LVM (montagem de volume lógico) para todas as três máquinas virtuais. Confira [Guia de início rápido para o Serviceguard para Linux (HPE)](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us)

* Verifique se você tem um runtime Java OpenJDK instalado nas VMs.

   > [!NOTE]
   > O SDK do Java da IBM não é compatível.

## <a name="install-sql-server"></a>Instale o SQL Server

Em todas as três VMs, siga uma das etapas abaixo com base na distribuição do Linux que você escolher para este tutorial, a fim de instalar o SQL Server e as ferramentas.

### <a name="rhel"></a>RHEL

* [Instalar o SQL Server no Red Hat](quickstart-install-connect-red-hat.md#install)
* [Ferramentas](quickstart-install-connect-red-hat.md#tools)

### <a name="sles"></a>SLES

* [Instalar o SQL Server no SLES](quickstart-install-connect-suse.md#install)
* [Ferramentas](quickstart-install-connect-suse.md#tools)

Depois de concluir esta etapa, você deve ter o serviço e as ferramentas do SQL Server instalados em todas as três VMs que participarão do grupo de disponibilidade.

## <a name="install-hpe-serviceguard-on-the-vms"></a>Instalar o HPE Serviceguard nas VMs

Nesta etapa, instale o HPE Serviceguard para Linux em todas as três VMs. A tabela a seguir descreve a função que cada servidor desempenha no cluster.

|Número de VMs | Função do HPE Serviceguard | Função da réplica de grupo de disponibilidade do Microsoft SQL Server|
|--------------|-----------------|------------|
|1 | Nós de cluster do HPE Serviceguard | Réplica primária |
|1 ou mais | Nó de cluster do HPE Serviceguard | Réplica secundária |
|1 | Servidor de quorum do HPE Serviceguard | Réplica somente de configuração |

Para instalar o Serviceguard, use o método `cminstaller`. Instruções específicas estão disponíveis nos links abaixo:

Cluster do Serviceguard e servidor de quorum do Serviceguard

* [Instale o Serviceguard para Linux em dois nós](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Install_serviceguard_using_cminstaller). Consulte a seção **Install_serviceguard_using_cminstaller**.
* [Instale o servidor de quorum do Serviceguard no terceiro nó](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Install_QS_from_the_ISO). Consulte a seção **Install_QS_from_the_ISO**.

Depois de concluir a instalação do cluster do HPE Serviceguard, você poderá habilitar o portal de gerenciamento de cluster na porta TCP 5522 no nó da réplica primária. As etapas a seguir adicionam uma regra ao firewall para permitir a porta 5522. O comando abaixo é para uma distribuição RHEL, você precisará executar comandos semelhantes para outras distribuições:

```console
sudo firewall-cmd --zone=public --add-port=5522/tcp --permanent

sudo firewall-cmd --reload 
```

## <a name="create-hpe-serviceguard-cluster"></a>Criar um cluster do HPE Serviceguard

Siga as instruções abaixo para configurar e criar o cluster do HPE Serviceguard. Nesta etapa, também configuraremos o servidor de quorum.

1. [Configure o servidor de quorum do Serviceguard no terceiro nó](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Configure_QS). Consulte a seção **Configure_QS**.
2. [Configure e crie o cluster do Serviceguard nos outros dois nós](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Configure_and_create_cluster). Consulte a seção **Configure_and_create_Cluster**.

## <a name="create-the-availability-group-and-add-a-sample-database"></a>Criar o grupo de disponibilidade e adicionar um banco de dados de exemplo

Nessa etapa, crie um grupo de disponibilidade com duas (ou mais) réplicas síncronas e uma réplica somente de configuração, que fornece proteção de dados e também pode fornecer alta disponibilidade. O seguinte diagrama representa essa arquitetura:

:::image type="content" source="media/sql-server-linux-availability-group-ha/2-configuration-only.png" alt-text="A réplica primária sincroniza dados do usuário e dados de configuração com a réplica secundária. A réplica primária sincroniza apenas os dados de configuração com a réplica somente de configuração. A réplica somente de configuração não tem réplicas de dados de usuário.":::

1. Replicação síncrona de dados do usuário para a réplica secundária. Ela também inclui metadados de configuração do grupo de disponibilidade.

2. Replicação síncrona de metadados de configuração do grupo de disponibilidade. Ela não inclui dados do usuário.

Para obter mais detalhes, consulte [Duas réplicas síncronas e uma réplica somente de configuração](sql-server-linux-availability-group-ha.md).

Para criar o grupo de disponibilidade, siga estas etapas:

1. [Habilite grupos de disponibilidade Always On e reinicie o MSSQL Server](#enable-always-on-availability-groups-and-restart-mssql-server) em todas as VMs, incluindo a réplica somente de configuração.
2. [Habilitar uma sessão de evento `AlwaysOn_health` – (Opcional)](#enable-an-alwayson_health-event-session---optional)
3. [Criar um certificado na VM primária](#create-a-certificate-on-the-primary-vm)
4. [Criar o certificado em servidores secundários](#create-the-certificate-on-secondary-servers)
5. [Criar os pontos de extremidade de espelhamento de banco de dados nas réplicas](#create-the-database-mirroring-endpoints-on-the-replicas)
6. [Criar grupo de disponibilidade](#create-availability-group)
7. [Ingressar as réplicas secundárias](#join-the-secondary-replicas)
8. [Adicionar um banco de dados ao grupo de disponibilidade criado acima](#add-a-database-to-the-availability-group-created-above)

### <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Habilitar grupos de disponibilidade Always On e reiniciar o mssql-server

Habilite o recurso Always On em todos os nós que hospedam uma instância do SQL Server. Em seguida, reinicie o mssql-server. Execute seguinte script em todos os três nós:

```console
sudo /opt/mssql/bin/mssql-conf
set hadr.hadrenabled 1 sudo systemctl restart mssql-serve
```

### <a name="enable-an-alwayson_health-event-session---optional"></a>Habilitar uma sessão de evento `AlwaysOn_health` – (Opcional)

Opcionalmente, é possível habilitar eventos estendidos de grupos de disponibilidade AlwaysOn para ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade. Execute o seguinte comando em cada instância do SQL Server:

```tsql
ALTER EVENT SESSION AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

### <a name="create-a-certificate-on-the-primary-vm"></a>Criar um certificado na VM primária

O script Transact-SQL a seguir cria uma chave mestra e um certificado. Em seguida, ele faz backup do certificado e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Conecte-se à instância primária do SQL Server e execute o seguinte script Transact-SQL:

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Master_Key_Password';

CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';

BACKUP CERTIFICATE dbm_certificate TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
WITH PRIVATE KEY 
    ( FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
      ENCRYPTION BY PASSWORD = '<Private_Key_Password>' );

```

Nesse momento, a réplica primária do SQL Server tem um certificado em `/var/opt/mssql/data/dbm_certificate.cer` e uma chave privada em `var/opt/mssql/data/dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedarão as réplicas de disponibilidade. Use o usuário mssql ou conceda permissão ao usuário mssql para acessar esses arquivos.

Por exemplo, no servidor de origem, o comando a seguir copia os arquivos para o computador de destino. Substitua os valores de `'node2'` pelo nome do host que executa a instância secundária do SQL Server. Copie o certificado na réplica somente de configuração também e execute os comandos abaixo também nesse nó.

```console
cd /var/opt/mssql/data
scp dbm_certificate.* root@<node2>:/var/opt/mssql/data/
```

Agora, nas VMs secundárias que executam a instância secundária e a réplica somente de configuração do SQL Server, execute os comandos abaixo para que o usuário do MSSQL possa ser o proprietário do certificado copiado:

```console
cd /var/opt/mssql/data

chown mssql:mssql dbm_certificate.*
```

### <a name="create-the-certificate-on-secondary-servers"></a>Criar o certificado em servidores secundários

O script Transact-SQL a seguir cria uma chave mestra e um certificado com base no backup que você criou na réplica primária do SQL Server. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo. pvk em uma etapa anterior. Para criar o certificado, execute o script a seguir em todos os servidores secundários, exceto na réplica somente de configuração:

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD =
'<Master_Key_Password>';

CREATE CERTIFICATE dbm_certificate FROM FILE =
'/var/opt/mssql/data/dbm_certificate.cer'
WITH PRIVATE KEY ( FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
DECRYPTION BY PASSWORD = '<Private_Key_Password>' );
```

### <a name="create-the-database-mirroring-endpoints-on-the-replicas"></a>Criar os pontos de extremidade de espelhamento de banco de dados nas réplicas

Na réplica primária e secundária, execute os seguintes comandos para criar os pontos de extremidade de espelhamento de banco de dados:

```tsql
CREATE ENDPOINT [hadr_endpoint] AS TCP (LISTENER_PORT = 5022)
    FOR DATABASE_MIRRORING 
        (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );

ALTER ENDPOINT [hadr_endpoint] STATE = STARTED;
```

> [!NOTE]
> 5022 é a porta padrão usada para o ponto de extremidade de espelhamento de banco de dados, mas você pode alterá-la para qualquer porta disponível.

Na réplica somente de configuração, crie o ponto de extremidade de espelhamento de banco de dados usando o comando abaixo. Observe que o valor da função aqui é definido como `WITNESS`, que é o valor necessário para a réplica somente de configuração.

```tsql
CREATE ENDPOINT [hadr_endpoint] AS TCP (LISTENER_PORT = 5022)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );

ALTER ENDPOINT [hadr_endpoint] STATE = STARTED;
```

### <a name="create-availability-group"></a>Criar grupo de disponibilidade

Na instância da réplica primária, execute os comandos a seguir. Esses comandos criam um grupo de disponibilidade chamado **ag1**, que tem um `cluster_type` **externo** e concede permissão para de criação de banco de dados ao grupo de disponibilidade.

Antes de executar os scripts a seguir, substitua os espaços reservados `<node1>`, `<node2>` e `<node3>` (réplica somente de configuração) pelo nome das VMs que você criou nas etapas anteriores.

```tsql
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR REPLICA ON
    N'<node1>' WITH (
        ENDPOINT_URL = N'tcp://<node1>:<5022>',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = EXTERNAL,
        SEEDING_MODE = AUTOMATIC
        ),

    N'<node2>' WITH (
        ENDPOINT_URL = N'tcp://<node2>:\<5022>',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = EXTERNAL,
        SEEDING_MODE = AUTOMATIC
        ),
    
    N'<node3>' WITH (
        ENDPOINT_URL = N'tcp://<node3>:<5022>',
        AVAILABILITY_MODE = CONFIGURATION_ONLY
        );
          
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-the-secondary-replicas"></a>Ingressar as réplicas secundárias

Execute os comandos abaixo em todas as réplicas secundárias. Esses comandos ingressam as réplicas secundárias no grupo de disponibilidade "ag1" com a réplica primária e permitem acesso de criação de banco de dados ao grupo de disponibilidade ag1.

```tsql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
GO
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
GO
```

### <a name="add-a-database-to-the-availability-group-created-above"></a>Adicionar um banco de dados ao grupo de disponibilidade criado acima

Conecte-se à réplica primária e execute os comandos T-SQL abaixo para:

1. Criar um banco de dados de exemplo chamado **db1**, que será adicionado ao grupo de disponibilidade.
2. Definir o modelo de recuperação do banco de dados para completo. Todos os bancos de dados em um grupo de disponibilidade requerem o modelo de recuperação completa.
3. Fazer backup do banco de dados. Um banco de dados requer pelo menos um backup completo para que você possa adicioná-lo a um grupo de disponibilidade.

```tsql
CREATE DATABASE [db1]; -- creates a database named db1
GO
ALTER DATABASE [db1] SET RECOVERY FULL; -- set the database in full recovery mode
GO
BACKUP DATABASE [db1] -- backs up the database to disk TO DISK = N'/var/opt/mssql/data/db1.bak';
GO
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1]; -- adds the database db1 to the AG
GO
```

Depois de concluir com êxito as etapas anteriores, você pode ver um grupo de disponibilidade **ag1** criado e as três VMs são adicionadas como réplicas com uma réplica primária, uma réplica secundária e uma réplica somente de configuração. **ag1** contém um banco de dados.

## <a name="deploy-the-sql-server-availability-group-workload-hpe-cluster-manager"></a>Implantar a carga de trabalho do grupo de disponibilidade do SQL Server (Gerenciador de Cluster HPE)

No HPE Serviceguard, implante a carga de trabalho do SQL Server no grupo de disponibilidade por meio da interface do usuário do gerenciador de cluster do Serviceguard.
   
Implante a carga de trabalho do grupo de disponibilidade e habilite a HA (alta disponibilidade), DR (recuperação de desastre) via cluster do Serviceguard usando a [interface gráfica do usuário do gerenciador do Serviceguard](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Protect_your_alwayson_availability_group). Consulte a seção **Proteger grupos de disponibilidade Always On do Microsoft SQL Server em Linux**.

## <a name="perform-automatic-failover-and-join-the-node-back-to-cluster"></a>Realizar um failover automático e ingressar o nó de volta no cluster

Para o teste de failover automático, você pode desativar a réplica primária (desligar). Isso replicará a indisponibilidade repentina do nó primário. O comportamento esperado é:

1. O gerenciador de cluster promove uma das réplicas secundárias no grupo de disponibilidade para primária.
2. A réplica primária com falha é ingressada automaticamente no cluster após o backup dela ser realizado. O gerenciador de cluster promove-a para réplica secundária.

Para o HPE Serviceguard, consulte a seção [**Testar a configuração para prontidão de failover**](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Test_the_setup_preparedness)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [Grupos de disponibilidade Always On no Linux](sql-server-linux-availability-group-overview.md).
