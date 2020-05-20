---
title: Solucionar problemas de configuração de Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [SQL Server], deploying
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], configuring
ms.assetid: 8c222f98-7392-4faf-b7ad-5fb60ffa237e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5041882c3eadb4e7f6f28a118e45c6e42f13cea6
ms.sourcegitcommit: 5a9ec5e28543f106bf9e7aa30dd0a726bb750e25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2020
ms.locfileid: "82924883"
---
# <a name="troubleshoot-alwayson-availability-groups-configuration-sql-server"></a>Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn (SQL Server)
  Este tópico fornece informações para ajudar a solucionar problemas típicos ao configurar instâncias de servidor para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Os problemas de configuração típicos incluem: o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está desabilitado, as contas estão configuradas incorretamente, o ponto de extremidade de espelhamento de banco de dados não existe, o ponto de extremidade está inacessível (Erro 1418 do SQL Server), o acesso à rede não existe e falha no comando de junção de banco de dados (Erro 35250 do SQL Server).

> [!NOTE]
>  Verifique se você está atendendo aos pré-requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter mais informações, consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).

 **Neste tópico:**

|Seção|Descrição|
|-------------|-----------------|
|[Os grupos de disponibilidade AlwaysOn não estão habilitados](#IsHadrEnabled)|Se uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não estiver habilitada para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], a instância não dará suporte à criação de grupo de disponibilidade e não poderá hospedar nenhuma réplica de disponibilidade.|
|[Contas](#Accounts)|Discute os requisitos para configurar corretamente as contas nas quais o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será executado.|
|[Pontos de extremidade](#Endpoints)|Discute como diagnosticar problemas com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor.|
|[Nome do sistema](#SystemName)|Resume as alternativas para especificar o nome do sistema de uma instância do servidor em uma URL de ponto de extremidade.|
|[Acesso à rede](#NetworkAccess)|Documenta o requisito de que cada instância do servidor que está hospedando uma réplica de disponibilidade deve poder acessar a porta de cada uma das instâncias do servidor sobre TCP.|
|[Acesso ao ponto de extremidade (erro 1418 do SQL Server)](#Msg1418)|Contém informações sobre essa mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|
|[Falha no banco de dados de junção (erro de SQL Server 35250)](#JoinDbFails)|Discute as possíveis causas e resolução de uma falha ao unir bancos de dados secundários a um grupo de disponibilidade porque a conexão com a réplica primária não está ativa.|
|[O roteamento somente leitura não está funcionando corretamente](#ROR)||
|[Tarefas relacionadas](#RelatedTasks)|Contém uma lista de tópicos orientados para tarefas nos Manuais Online do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que são particularmente relevantes para solucionar problemas de configuração de grupos de disponibilidade.|
|[Conteúdo relacionado](#RelatedContent)|Contém uma lista de recursos relevantes que são externos aos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|

##  <a name="alwayson-availability-groups-is-not-enabled"></a><a name="IsHadrEnabled"></a>Grupos de Disponibilidade AlwaysOn não está habilitado
 O recurso do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve estar habilitado em cada uma das instâncias do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md).

##  <a name="accounts"></a><a name="Accounts"></a>As
 As contas nas quais o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executado devem ser configuradas corretamente.

1.  As contas têm as permissões corretas?

    1.  Se os parceiros forem executados como a mesma conta de usuário do domínio, os logons de usuário corretos existirão automaticamente em ambos os bancos de dados **master** . Isso simplifica a configuração de segurança do banco de dados e é recomendado.

    2.  Se duas instâncias do servidor forem executadas como contas diferentes, o logon de cada conta deverá ser criado no banco de dados **master** na instância do servidor remoto e esse logon deverá receber permissões CONNECT para se conectar ao ponto de extremidade de espelhamento do banco de dados dessa instância do servidor. Para obter mais informações, consulte[Configurar contas de logon para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md).

2.  Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede ou uma conta que não pertença ao domínio, você deverá usar certificados para autenticação de ponto de extremidade. Se suas contas de serviço estiverem usando contas de domínio no mesmo domínio, você poderá escolher conceder acesso de CONNECT a cada conta de serviço em todos os locais de réplica ou usar certificados. Para obter mais informações, veja [Usar certificados para um ponto de extremidade do espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).

##  <a name="endpoints"></a><a name="Endpoints"></a> Pontos de extremidade
 Os pontos de extremidade devem ser configurados corretamente.

1.  Verifique se cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que vai hospedar uma réplica de disponibilidade (cada *local de réplica*) tem um ponto de extremidade de espelhamento de banco de dados. Para determinar se existe um ponto de extremidade de espelhamento do banco de dados em determinada instância do servidor, use a exibição de catálogo [sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql). Para obter mais informações, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) ou [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).

2.  Verifique se os números da porta estão corretos.

     Para identificar a porta associada atualmente com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor, use a seguinte instrução do [!INCLUDE[tsql](../../../includes/tsql-md.md)] :

    ```
    SELECT type_desc, port FROM sys.tcp_endpoints;
    GO
    ```

3.  Para os problemas da configuração do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] que forem difíceis de explicar, recomendamos que você inspecione cada instância do servidor para determinar se ela está escutando nas portas corretas. Para obter mais informações sobre como verificar a disponibilidade de porta, veja [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md).

4.  Verifique se os pontos de extremidade foram iniciados (STATE=STARTED). Em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]:

    ```
    SELECT state_desc FROM sys.database_mirroring_endpoints
    ```

     Para obter mais informações sobre a coluna **state_desc**, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql).

     Para iniciar um ponto de extremidade, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]:

    ```
    ALTER ENDPOINT Endpoint_Mirroring 
    STATE = STARTED 
    AS TCP (LISTENER_PORT = <port_number>)
    FOR database_mirroring (ROLE = ALL);
    GO
    ```

     Para obter mais informações, consulte [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).

5.  Verifique se o logon do outro servidor tem permissão CONNECT. Para determinar quem tem permissão CONNECT para um ponto de extremidade, em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] :

    ```
    SELECT 'Metadata Check';
    SELECT EP.name, SP.STATE, 
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id)) 
          AS GRANTOR, 
       SP.TYPE AS PERMISSION,
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id)) 
          AS GRANTEE 
       FROM sys.server_permissions SP , sys.endpoints EP
       WHERE SP.major_id = EP.endpoint_id
       ORDER BY Permission,grantor, grantee; 
    GO

    ```

##  <a name="system-name"></a><a name="SystemName"></a> System Name
 Para o nome de sistema de uma instância do servidor em uma URL de ponto de extremidade, você pode usar qualquer nome que identifique o sistema inequivocamente. O endereço de servidor pode ser um nome de sistema (se os sistemas estiverem no mesmo domínio), um nome de domínio totalmente qualificado ou um endereço de IP (preferivelmente, um endereço de IP estático). Usando o nome de domínio totalmente qualificado o funcionamento é garantido. Para obter mais informações, consulte [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).

##  <a name="network-access"></a><a name="NetworkAccess"></a> Network Access
 Cada instância do servidor que esteja hospedando uma réplica de disponibilidade deve poder acessar a porta de cada uma das instâncias do servidor sobre TCP. Isso será especialmente importante se as instâncias do servidor estiverem em domínios diferentes que não confiam um no outro (domínios não confiáveis).

##  <a name="endpoint-access-sql-server-error-1418"></a><a name="Msg1418"></a> Acesso ao ponto de extremidade (erro 1418 do SQL Server)
 Essa mensagem do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] indica que o endereço de rede do servidor especificado na URL do ponto de extremidade não pode ser atingido ou não existe e sugere que você verifique o nome do endereço de rede e emita o comando novamente. Para obter mais informações, veja [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md).

##  <a name="join-database-fails-sql-server-error-35250"></a><a name="JoinDbFails"></a> Falha ao unir bancos de dados (erro 35250 do SQL Server)
 Discute as possíveis causas e resolução de uma falha ao unir bancos de dados secundários a um grupo de disponibilidade porque a conexão com a réplica primária não está ativa.

 **Resolução:**

1.  Verifique a configuração do firewall para confirmar se ele permite comunicação da porta do ponto de extremidade entre as instâncias do servidor que hospedam a réplica primária e a réplica secundária (por padrão, a porta 5022).

2.  Verifique se a conta de serviço de rede tem permissão para conectar-se ao ponto de extremidade.

##  <a name="read-only-routing-is-not-working-correctly"></a><a name="ROR"></a>O roteamento somente leitura não está funcionando corretamente
 Verifique as configurações de valores a seguir e corrija-as se necessário.

||Ligado...|Ação|Comentários|Link|
|------|---------|------------|--------------|----------|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Réplica primária atual|Verifique se o ouvinte do grupo de disponibilidade está online.|**Para verificar se o ouvinte está online:**<br /><br /> `SELECT * FROM sys.dm_tcp_listener_states;`<br /><br /> **Para reiniciar um ouvinte offline:**<br /><br /> `ALTER AVAILABILITY GROUP myAG RESTART LISTENER 'myAG_Listener';`|[sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Réplica primária atual|Verifique se READ_ONLY_ROUTING_LIST contém somente instâncias de servidor que hospedem uma réplica secundária legível.|**Para identificar réplicas secundárias legíveis:** sys.availability_replicas (coluna**secondary_role_allow_connections_desc** )<br /><br /> **Para exibir uma lista de roteamento somente leitura:** sys.availability_read_only_routing_lists<br /><br /> **Para alterar uma lista de roteamento somente leitura:** ALTER AVAILABILITY GROUP|[sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Cada réplica em read_only_routing_list|Verifique se o firewall do Windows não está bloqueando a porta READ_ONLY_ROUTING_URL.|-|[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Cada réplica em read_only_routing_list|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager, verifique se:<br /><br /> A conectividade remota do SQL Server está habilitada.<br /><br /> TCP/IP está habilitado.<br /><br /> Os endereços IP estão configurados corretamente.|-|[Exibir ou alterar as propriedades de servidor &#40;SQL Server&#41;](../../configure-windows/view-or-change-server-properties-sql-server.md)<br /><br /> [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Cada réplica em read_only_routing_list|Verifique se a READ_ONLY_ROUTING_URL (TCP<strong>:// *`system-address`* :</strong>*Port*) contém o FQDN (nome de domínio totalmente qualificado) e o número da porta corretos.|-|[Calculando read_only_routing_url de AlwaysOn](https://docs.microsoft.com/archive/blogs/mattn/calculating-read_only_routing_url-for-alwayson)<br /><br /> [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Verificação](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sistema cliente|Verifique se o driver cliente dá suporte a roteamento somente leitura.|-|[Conectividade de Cliente AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)|

##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas

-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)

-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)

-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)

-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)

-   [Solucionar problemas de uma operação de adição de arquivo com falha &#40;Grupos de Disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)

-   [Gerenciamento de logons e trabalhos para os bancos de dados de um grupo de disponibilidade &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)

-   [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)

##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado

-   [Exibir eventos e logs de um cluster de failover](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)

-   [Cluster de failover Get-ClusterLog do cmdlet](https://technet.microsoft.com/library/ee461045.aspx)

-   [Blog da equipe do AlwaysOn do SQL Server: blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)

## <a name="see-also"></a>Consulte Também
 [Segurança de transporte para espelhamento de banco de dados e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md) pré-requisitos de [configuração de rede do cliente](../../configure-windows/client-network-configuration.md) [, restrições e recomendações para grupos de disponibilidade AlwaysOn](prereqs-restrictions-recommendations-always-on-availability.md) &#40;SQL Server&#41;


