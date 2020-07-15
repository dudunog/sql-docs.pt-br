---
title: 'Assistente do Grupo de Disponibilidade: Página Especificar Réplicas'
description: Descreve as opções da página Especificar Réplicas do Assistente de Novo Grupo de Disponibilidade no SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.listeners.f1
- sql13.swb.addreplicawizard.specifyreplicas.f1
- sql13.swb.newagwizard.specifyreplicas.f1
ms.assetid: 2d90fc12-a67b-4bd0-b0ab-899b73017196
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9a278ecf99626aef66dde768c18e8577dbb39c94
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898093"
---
# <a name="specify-replicas-page-new-availability-group-wizard-add-replica-wizard"></a>Página Especificar réplicas (Assistente de novo grupo de disponibilidade: assistente para adicionar réplica)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve as opções da página **Especificar Réplicas** . Essa página aplica-se ao **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]** e ao **[!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]** . Use a página **Especificar Réplicas** para especificar e configurar uma ou mais réplicas de disponibilidade para adicionar o grupo de disponibilidade. Essa página contém quatro guias que são apresentadas na tabela a seguir. Clique no nome de uma guia na tabela para ir para a seção correspondente, mais adiante neste tópico.  
  
|Tab|Breve descrição|  
|---------|-----------------------|  
|[Réplicas](#ReplicasTab)|Use esta guia para especificar cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará ou que hospeda uma réplica secundária. Observe que a instância de servidor à qual você está conectado no momento deve hospedar a réplica primária.<br /><br /> Termine de especificar todas as réplicas na guia **Réplicas** antes de iniciar as outras guias.<br/><br/> Observação O **failover automático** será desabilitado se o tipo de cluster for **NONE**. O SQL Server dá suporte apenas ao failover manual quando um grupo de disponibilidade não está em um cluster. <br/><br/> Quando o tipo de cluster é EXTERNAL, o modo de failover é **Externo**. <br/><br/> Ao adicionar uma réplica, todas as novas réplicas devem ser hospedadas no mesmo tipo de sistema operacional das réplicas existentes. <br/><br/>Ao adicionar uma réplica, se a réplica primária estiver em um WSFC, as réplicas secundárias deverão estar no mesmo cluster.|
|[Pontos de extremidade](#EndpointsTab)|Use esta guia para verificar quaisquer pontos de extremidade de espelhamento de banco de dados existentes e também, se esse ponto de extremidade estiver ausente em uma instância de servidor cujas contas de serviço usam a Autenticação do Windows para criar o ponto de extremidade automaticamente.|  
|[Preferências de backup](#BackupPreferencesTab)|Use esta guia para especificar sua preferência de backup para o grupo de disponibilidade como um todo e suas prioridades de backup para as réplicas de disponibilidade individuais.|  
|[Ouvinte](#Listener)|Use esta guia, se disponível, para criar um ouvinte de grupo de disponibilidade. Por padrão, não é criado um ouvinte.<br /><br /> Esta guia estará disponível apenas se você estiver executando o [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)].<br/><br/>O DHCP está desabilitado quando o tipo de cluster é EXTERNAL ou NONE. |  
  
##  <a name="replicas-tab"></a><a name="ReplicasTab"></a> Guia Réplicas  
 **Instância do Servidor**  
 Exibe o nome da instância de servidor que hospedará a réplica de disponibilidade.  
  
 Se uma instância de servidor que você pretende usar para hospedar uma réplica secundária não estiver listada na grade **Réplicas de Disponibilidade**, clique no botão **Adicionar Réplica**. Para configurar um grupo de disponibilidade em um ambiente de TI híbrido (confira [Alta disponibilidade e recuperação de desastre para SQL Server nas Máquinas Virtuais do Azure](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)), clique no botão **Adicionar Réplica do Azure** para criar máquinas virtuais com réplicas secundárias no Azure.  
  
 **Função inicial**  
 Indica a função que a nova réplica executará inicialmente: **Primária** ou **secundária**.  
  
 **Failover Automático (Até 3)**  
 Marque esta caixa de seleção se você desejar que esta réplica de disponibilidade seja um parceiro de failover automático. Para configurar o failover automático, você deve escolher essa opção para a réplica primária inicial e para uma réplica secundária. Essas duas réplicas usarão o modo de disponibilidade da confirmação síncrona. Apenas três réplicas podem dar suporte ao failover automático.  
  
 Para obter mais informações sobre o modo de disponibilidade de confirmação síncrona, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). Para obter informações sobre failover automático, consulte [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 **Confirmação Síncrona (até 3)**  
 Se você tiver selecionado **Failover Automático (Até 3)** para a réplica, **Confirmação Síncrona (Até 3)** também será selecionada. Se a caixa de seleção estiver em branco, selecione-a apenas se desejar que esta réplica use o modo de confirmação síncrona com failover manual planejado apenas. Apenas três réplicas podem usar o modo de confirmação síncrona.  
  
 Se desejar que esta réplica use o modo de disponibilidade de confirmação assíncrona, deixe essa caixa de seleção em branco. A réplica dará suporte apenas a failover manual forçado (com possível perda de dados). Para obter mais informações sobre o modo de disponibilidade de confirmação assíncrona, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). Para obter informações sobre o failover manual planejado e o failover manual forçado, consulte [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 **Função Secundária Legível**  
 Selecione um valor na lista suspensa **Secundária Legível** , da seguinte forma:  
  
 **Não**  
 Nenhuma conexão direta é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
 **Tentativa de leitura somente**  
 Somente conexões diretas somente leitura são permitidas para bancos de dados secundários desta réplica. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 **Sim**  
 Todas as conexões são permitidas para os bancos de dados secundários desta réplica, mas somente para acesso de leitura. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 **Adicionar Réplica**  
 Clique para adicionar uma réplica secundária ao grupo de disponibilidade.  
  
 **Adicionar Réplica do Azure**  
 Clique para criar uma máquina virtual do Azure que esteja executando uma réplica secundária no grupo de disponibilidade. Esta opção é aplicável apenas a um grupo de disponibilidade em TI híbrida que contenha réplicas locais. Para obter mais informações, confira [Alta disponibilidade e recuperação de desastres para o SQL Server em Máquinas Virtuais do Azure](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx).  
  
 **Remover Réplica**  
 Clique para remover a réplica secundária especificada do grupo de disponibilidade.  
  
##  <a name="endpoints-tab"></a><a name="EndpointsTab"></a> Guia Pontos de Extremidade  
 Para cada instância de servidor que hospedará uma réplica de disponibilidade, a guia **Pontos de Extremidade** exibirá valores reais do ponto de extremidade de espelhamento de banco de dados existente, se houver algum, ou valores sugeridos para um novo ponto de extremidade potencial que usaria a Autenticação do Windows. Para os pontos de extremidade existentes e potenciais, a grade Valores do ponto de extremidade exibe as seguintes informações:  
  
 **Nome do servidor**  
 Exibe o nome de uma instância de servidor que hospedará uma réplica de disponibilidade.  
  
 **URL do Ponto de Extremidade**  
 Exibe a URL real ou proposta do ponto de extremidade de espelhamento do banco de dados. Para um novo ponto de extremidade proposto, você pode alterar esse valor. Para obter informações sobre o formato dessas URLs, veja [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Número da Porta**  
 Exibe a URL real ou proposta do número da porta do ponto de extremidade. Para um novo ponto de extremidade proposto, você pode alterar esse valor.  
  
 **Nome do Ponto de Extremidade**  
 Exibe o nome real ou proposto do ponto de extremidade. Para um novo ponto de extremidade proposto, você pode alterar esse valor.  
  
 **Criptografar Dados**  
 Indica se os dados enviados por este ponto de extremidade estão criptografados. Para um novo ponto de extremidade proposto, você pode alterar essa configuração.  
  
 **Conta de Serviço do SQL Server**  
 Nome de usuário da conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para que uma instância de servidor use um ponto de extremidade que usa a Autenticação do Windows, sua conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser uma conta de domínio.  
  
 Esse requisito determina sua próxima etapa de configuração, da seguinte maneira:  
  
-   Se cada instância de servidor estiver sendo executada em uma conta de serviço de domínio, ou seja, se a coluna **Conta de Serviço do SQL Server** exibir uma conta de serviço de domínio para cada instância de servidor, clique em **Avançar**.  
  
-   Se alguma instância de servidor estiver sendo executada em uma conta de serviço que não pertence a um domínio, você precisará fazer uma alteração manual na instância de servidor para que possa continuar as etapas do assistente. Nesse caso, quando você clicar em **Avançar** , será exibida uma caixa de diálogo de aviso. Clique em **Não**para retornar à guia**Pontos de Extremidade** . Enquanto estiver saindo do assistente na página **Especificar Réplicas** , faça um das seguintes alterações em cada instância de servidor para a qual a coluna **Conta de Serviço do SQL Server** exiba uma conta de serviço que não pertence a um domínio:  
  
    -   Use o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para transformar a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma conta de domínio. Para obter mais informações, consulte [Alterar a conta de inicialização do serviço SQL Server &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/scm-services-change-the-service-startup-account.md).  
  
    -   Use o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell para criar manualmente um ponto de extremidade de espelhamento de banco de dados que usa um certificado. Para obter mais informações, consulte [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md) ou [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md).  
  
     Se você deixar a página **Especificar Réplicas de Disponibilidade** aberta enquanto configura pontos de extremidade, retorne à guia **Pontos de Extremidade** e clique em **Atualizar** para atualizar a grade **Valores do ponto de extremidade** .  
  
##  <a name="backup-preferences-tab"></a><a name="BackupPreferencesTab"></a> Guia Preferências de Backup  
 Para especificar onde os backups devem ocorrer, escolha uma das opções a seguir:  
  
 **Preferir Secundário**  
 Especifica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online. Nesse caso, o backup deve ocorrer na réplica primária. Essa é a opção padrão.  
  
 **Somente Secundário**  
 Especifica que os backups nunca devem ser executados na réplica primária. Se a réplica primária for a única réplica online, o backup não deveria ocorrer.  
  
 **Primário**  
 Especifica que os backups sempre devem ocorrer na réplica primária. Essa opção será útil se você precisar de recursos de backup, como a criação de backups diferenciais, que não têm suporte quando o backup é executado em uma réplica secundária.  
  
 **Qualquer Réplica**  
 Especifica que você prefere que trabalhos de backup ignorem a função das réplicas de disponibilidade ao escolher a réplica para executar backups. Observe que os trabalhos de backup podem avaliar outros fatores, como prioridade de backup de cada réplica de disponibilidade em combinação com seu estado operacional e estado conectado.  
  
> [!IMPORTANT]  
>  Não há nenhuma imposição da configuração de preferência de backup. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. Para obter mais informações, confira [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
### <a name="replica-backup-priorities-grid"></a>Grade Prioridades de backup de réplica  
 Use a grade **Prioridades de backup de réplica** para especificar suas prioridades de backup para cada uma das réplicas do grupo de disponibilidade. Essa grade contém as seguintes colunas:  
  
 **Instância do Servidor**  
 Exibe o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade.  
  
 **Prioridade de Backup (Mais Baixa = 1, Mais Alta = 100)**  
 Atribua a prioridade para backups que estão sendo executados nesta réplica em relação a outras réplicas no mesmo grupo de disponibilidade. O valor padrão é 50. Você pode selecionar qualquer outro inteiro no intervalo de 0 a 100. 1 indica a prioridade mais baixa, e 100 indica a prioridade mais alta. Se você definir a **Prioridade de Backup** como 1, a réplica de disponibilidade será escolhida para executar backups apenas se nenhuma réplica de disponibilidade de prioridade mais alta estiver disponível no momento.  
  
 **Excluir Réplica**  
 Para evitar que esta réplica de disponibilidade seja escolhida para execução de backups. Isso é útil, por exemplo, para uma réplica de disponibilidade remota para a qual você nunca deseja que ocorra o failover de backups.  
  
##  <a name="listener-tab"></a><a name="Listener"></a> Guia Ouvinte  
 Especifique sua preferência para um[ouvinte de grupo de disponibilidade](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)que fornecerá um ponto de conexão de cliente entre as seguintes opções:  
  
 **Não crie um ouvinte de grupo de disponibilidade agora.**  
 Selecione para ignorar esta etapa. Você pode criar um ouvinte posteriormente. Para obter mais informações, consulte [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **Criar um ouvinte de grupo de disponibilidade.**  
 Especifique suas preferências de ouvinte para este grupo de disponibilidade, da seguinte maneira:  
  
 **Nome DNS do Ouvinte**  
 Especifique o nome da rede do ouvinte. Esse nome deve ser exclusivo no domínio e pode conter apenas caracteres alfanuméricos, traços ( **-** ) e hifens ( **_** ), em qualquer ordem. Quando especificado usando a guia **Ouvinte** , o nome DNS pode ter até 15 caracteres de comprimento.  
  
> [!IMPORTANT]  
>  Se você inserir um nome de ouvinte DNS inválido (ou número da porta) na guia **Ouvinte** , o botão **Avançar** será desabilitado na página **Especificar Réplicas** .  
  
 **Porta**  
 Especifique a porta TPC usada por esse ouvinte.  
  
> [!NOTE]  
>  Se você inserir um número da porta (ou nome de ouvinte DNS) inválido na guia **Ouvinte** , o botão **Avançar** será desabilitado na página **Especificar Réplicas** .  
  
 **Modo de Rede**  
 Use a lista suspensa para selecionar o modo de rede a ser usado por este ouvinte, um dos seguintes:  
  
 **IP Estático**  
 Selecione se você deseja que o ouvinte escute em mais de uma sub-rede. Para usar o modo de rede IP estático, um ouvinte de grupo de disponibilidade deve escutar em toda sub-rede que hospeda uma réplica de disponibilidade para o grupo de disponibilidade. Para cada sub-rede, clique em **Adicionar** para selecionar um endereço de sub-rede e especificar um endereço IP.  
  
 Se **IP Estático** for selecionado como o modo de rede (esta é a seleção padrão), uma grade exibirá as colunas **Sub-rede** e **Endereço IP** e os botões **Adicionar** e **Remover** associados serão exibidos. A grade estará vazia até que você adicione a primeira sub-rede.  
  
 Coluna**Sub-rede**  
 Exibe o endereço de sub-rede que você selecionou para cada sub-rede adicionada para o ouvinte.  
  
 Coluna**Endereço IP**  
 Exibe o endereço IPv4 ou IPv6 que você especificou para uma determinada sub-rede.  
  
 **Adicionar**  
 Clique para adicionar uma sub-rede a este ouvinte. Essa ação abre a caixa de diálogo **Adicionar Endereço IP** . Para obter mais informações, consulte o tópico de ajuda [Caixa de diálogo Adicionar Endereço IP &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md).  
  
 **Remover**  
 Clique para remover a sub-rede que está selecionada atualmente na grade.  
  
 **DHCP**  
 Selecione se desejar que o ouvinte escute em uma única sub-rede e para usar um endereço IPv4 dinâmico atribuído por um servidor que está executando o Protocolo DHCP. O DHCP é limitado a uma única sub-rede que é comum a cada instância de servidor que hospeda uma réplica de disponibilidade para o grupo de disponibilidade. O DHCP não está disponível para o tipo de cluster externo ou nenhum.  
  
> [!IMPORTANT]  
>  Nós não recomendamos o DHCP em ambiente de produção. Se houver um tempo de inatividade e a concessão do IP do DHCP expirar, a hora adicional deverá registrar o novo endereço IP da rede DHCP que está associado ao nome DNS do ouvinte e afetará a conectividade do cliente. No entanto, o DHCP é bom para configurar seu ambiente de desenvolvimento e teste para verificar as funções básicas de grupos de disponibilidade e para integração com seus aplicativos.  
  
 Quando **DHCP** é selecionado, o campo **Sub-rede** é exibido.  
  
 **Sub-rede**  
 Se você selecionou **DHCP** como o modo de rede, use a lista suspensa **Sub-rede** para selecionar um endereço para a sub-rede que hospeda as réplicas de disponibilidade do grupo de disponibilidade.  
  
> [!IMPORTANT]
>  Depois que você definir um ouvinte de grupo de disponibilidade, será altamente recomendável fazer o seguinte:  
> 
>  -   Peça ao administrador da rede para reservar o endereço IP do ouvinte para seu uso exclusivo. Informe o nome do host DNS do ouvinte aos desenvolvedores de aplicativos para uso em cadeias de conexão ao pedir conexões cliente com esse grupo de disponibilidade.  
> -   Informe o nome do host DNS do ouvinte aos desenvolvedores de aplicativos para uso em cadeias de conexão ao pedir conexões cliente com esse grupo de disponibilidade.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
