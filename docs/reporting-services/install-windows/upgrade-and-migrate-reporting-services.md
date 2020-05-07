---
title: Atualizar e migrar o Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
ms.topic: conceptual
ms.date: 05/01/2020
ms.openlocfilehash: ca9ffd01b7553cb343a83565615a786467371891
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719526"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Este tópico é uma visão geral das opções de atualização e migração do SQL Server Reporting Services. Veja as abordagens gerais para fazer upgrade de uma implantação do SQL Server Reporting Services:  
 
- **Atualizar *para* o Reporting Services 2016 e anteriores *do* Reporting Services 2016 e anteriores:** você atualiza os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos servidores e nas instâncias em que eles estão instalados atualmente. Isto é geralmente chamado de atualização “no local”. A atualização in-loco não tem suporte de um modo de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para outro. Por exemplo, você não pode atualizar um servidor de relatório de modo nativo para um servidor de relatório no modo do SharePoint. Você pode migrar seus itens de relatório de um modo para outro. Para obter mais informações, confira a seção [Cenários de atualização e migração do modo do SharePoint](#bkmk_sharePoint_scenarios) mais adiante neste documento.  

- **A atualização *para* o Reporting Services 2017 e posteriores *do* Reporting Services 2016 e anteriores** não é o mesmo cenário de atualização que as versões anteriores. Ao atualizar *para* o Reporting Services 2016 e anteriores, você pode seguir um processo de atualização in-loco usando a mídia de instalação do SQL Server. Ao atualizar *para* o Reporting Services 2017 e posteriores *do* Reporting Services 2016 e anteriores, não será possível seguir as mesmas etapas porque a nova instalação do Reporting Services é um produto autônomo. Ela deixou de fazer parte da mídia de instalação do SQL Server. 

    Para atualizar do Reporting Services 2016 e anteriores para o Reporting Services 2017 e posteriores, siga o artigo [Migrar uma Instalação do Reporting Services (modo nativo)](migrate-a-reporting-services-installation-native-mode.md), com o Reporting Services 2017 ou posteriores como instância de destino. 

- **A atualização *do* Reporting Services 2017 para versões futuras** é, novamente, um cenário de atualização in-loco, pois os GUIDs de instalação do produto são os mesmos. Execute o arquivo de instalação SQLServerReportingServices.exe para iniciar a atualização in-loco no servidor no qual o Reporting Services está instalado.
  
- **Migração**: você instala e configura um novo ambiente do SharePoint, copia seus itens de relatório e recursos para o novo ambiente e configura o novo ambiente para usar o conteúdo existente. Uma forma de nível inferior de migração é copiar os bancos de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , arquivos de configuração e, se estiver usando o modo do SharePoint, os bancos de dados de conteúdo do SharePoint.  


> [!NOTE]
> A integração do Reporting Services ao SharePoint não está disponível após o SQL Server 2016.
   
##  <a name="known-upgrade-issues-and-best-practices"></a><a name="bkmk_known_issues"></a> Problemas de atualização conhecidos e práticas recomendadas  
 Para obter uma lista detalhada das edições e versões com suporte que você pode atualizar, consulte [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
> [!TIP]  
>  Para obter as últimas informações sobre problemas com o SQL Server, confira as [Notas sobre a versão do SQL Server 2016](https://go.microsoft.com/fwlink/?LinkID=398124).  
  
  
##  <a name="side-by-side-installations"></a><a name="bkmk_side_by_side"></a> Instalações lado a lado  
 O modo Nativo do SQL Server Reporting Services pode ser instalado lado a lado com uma implantação no modo Nativo do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Não há suporte para implantações lado a lado do SQL Server Reporting Services no modo do SharePoint e para nenhuma das versões anteriores de componentes no modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
  
##  <a name="in-place-upgrade"></a><a name="bkmk_inplace_upgrade"></a> Atualização in-loco  
 A atualização é concluída pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usada para atualizar qualquer ou todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A Instalação detecta as instâncias existentes e solicita que você faça a atualização. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação fornece opções de atualização que podem ser especificadas como um argumento de linha de comando ou no Assistente de Instalação.  
  
 Quando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada, é possível selecionar a opção para atualizar uma das seguintes versões ou instalar uma nova instância do SQL Server Reporting Services que é executada lado a lado com instalações existentes:  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte o seguinte:  

* [Atualizar para o SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)
* [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)
  
  
##  <a name="pre-upgrade-checklist"></a><a name="bkmk_upgrade_checklist"></a> Lista de verificação anterior à atualização  
 Antes de fazer upgrade para o SQL Server Reporting Services, examine o seguinte:  
  
-   Examine os requisitos para determinar se o hardware e o software do computador podem dar suporte ao [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Para obter mais informações, veja [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Use o SCC (Verificador de Configuração do Sistema) para examinar o computador do servidor de relatório em busca de condições que podem impedir uma instalação bem-sucedida do SQL Server Reporting Services. Para obter mais informações, consulte [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   Consulte as práticas recomendadas e a orientação de segurança para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Faça backup da chave simétrica. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Faça backup dos bancos de dados do servidor de relatório e arquivos de configuração. Para obter mais informações, consulte [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md).  
  
-   Faça backup de quaisquer personalizações feitas em diretórios virtuais existentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no IIS.  
  
-   Remova certificados TLS/SSL inválidos.  Inclusive certificados expirados que você não planeja atualizar antes de atualizar o Reporting Services.  Certificados inválidos provocarão falha na atualização e uma mensagem de erro semelhante à seguinte será gravada no arquivo de log do Reporting Services: **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Não há um certificado SSL (protocolo SSL) configurado no site.** .  
  
 Antes de atualizar um ambiente de produção, execute sempre uma atualização de teste em um ambiente de pré-produção que tenha a mesma configuração do ambiente de produção.  
  
  
## <a name="overview-of-migration-scenarios"></a>Visão geral de cenários de migração  
 Se você estiver atualizando de uma versão com suporte do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente será possível executar o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar os arquivos de programa, o banco de dados e todos os dados de aplicativo do servidor de relatório.  
  
 No entanto, a **migração** manual de uma instalação do servidor de relatório será necessária se houver alguma das seguintes condições:  
  
-   Você quer alterar o tipo de servidor de relatório usado em sua implantação. Por exemplo, você não pode atualizar ou converter um servidor de relatório de modo nativo para um modo do SharePoint. Para obter mais informações, consulte [Migração do modo nativo para o SharePoint &#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).  
  
-   Você quer minimizar a quantidade de tempo que o servidor de relatório fica offline durante o processo de atualização. Sua instalação atual permanecerá online enquanto você copiar dados de conteúdo para uma nova instância do servidor de relatório e testar a instalação sem alterar o estado da instalação existente do servidor de relatório.  
  
-   Você deseja migrar uma implantação do SharePoint 2010 do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint 2013/2016. O SharePoint 2013/2016 não dá suporte à atualização in-loco do SharePoint 2010. Para obter mais informações, veja [Migrar uma instalação do Reporting Services &#40;Modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
  
##  <a name="native-mode-upgrade-and-migration-scenarios"></a><a name="bkmk_native_scenarios"></a> Atualização do modo nativo e cenários de migração  
 **Atualização:** a atualização in-loco para o modo nativo é o mesmo processo para cada uma das versões compatíveis listadas anteriormente neste tópico. Execute o assistente de instalação do SQL Server ou uma instalação pela linha de comando. Após a instalação, o banco de dados do servidor de relatório será automaticamente atualizado para o novo esquema de banco de dados do servidor de relatório. Para obter mais informações, veja a seção [Atualização in-loco](#bkmk_inplace_upgrade) neste tópico.  
  
 O processo de atualização começa quando você seleciona uma instância existente do servidor de relatório a ser atualizada.  
  
1.  Se o banco de dados do servidor de relatório estiver em um computador remoto e você não tiver permissão para atualizar esse banco de dados, a Instalação solicitará que você forneça credenciais para fazer a atualização para um banco de dados do servidor de relatório remoto. Certifique-se de fornecer credenciais que tenham permissões **sysadmin** ou de atualização de banco de dados.  
  
2.  A Instalação verifica se existem condições ou configurações que impedem a atualização e lê as definições de configuração. Os exemplos incluem extensões personalizadas implantadas no servidor de relatório. Se a atualização estiver bloqueada, você deverá modificar a instalação para que a atualização não seja mais bloqueada ou migrar para uma nova instância do SQL Server Reporting Services. Para obter mais informações, consulte a documentação do Supervisor de Atualização.  
  
3.  Se a atualização puder prosseguir, a Instalação solicitará que você continue o processo de atualização.  
  
4.  A Instalação cria novas pastas para arquivos de programa do SQL Server Reporting Services. As pastas de programa de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluem MSRS13.\<*instance name*>.  
  
5.  A Instalação adiciona os arquivos de programa, as ferramentas de configuração e os utilitários de linha de comando do servidor de relatório do SQL Server Reporting Services que fazem parte do recurso do servidor de relatório.  
  
    1.  Os arquivos de programas da versão anterior são removidos.  
  
    2.  Os utilitários e as ferramentas de configuração do servidor de relatório que são atualizados para a nova versão incluem a ferramenta Configuração do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os utilitários de linha de comando, por exemplo, RS.exe e o Construtor de Relatórios.  
  
    3.  Outras ferramentas cliente como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são um download separado e precisam ser atualizadas separadamente. Para obter mais informações, consulte [Baixar o SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx).
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é um download separado. Para obter mais informações, consulte [SQL Server Data Tools no Visual Studio 2015](https://msdn.microsoft.com/mt186501).  
  
6.  A Instalação reutiliza a entrada do serviço no Gerenciador de Controle de Serviço para o serviço Servidor de Relatório do SQL Server Reporting Services. Essa entrada de serviço inclui a conta de serviço Servidor de Relatório do Windows.  
  
7.  A Instalação reserva novas URLs com base nas configurações existentes do diretório virtual no IIS. A instalação pode não remover diretórios virtuais no IIS; portanto, remova-os manualmente depois que a atualização for concluída.  
  
8.  A Instalação mescla configurações nos arquivos de configuração. Quando você utiliza como base os arquivos de configuração da versão atual, são adicionadas novas entradas. As entradas obsoletas não são removidas, mas não serão mais lidas pelo servidor de relatório depois que a atualização for concluída. A atualização não excluirá arquivos de log antigos, o arquivo RSWebApplication.config obsoleto ou as configurações de diretório virtual no IIS. A atualização não removerá versões mais antigas do Designer de Relatórios, Management Studio ou outras ferramentas de cliente. Se você não mais precisar deles, certifique-se de remover esses arquivos e ferramentas depois que a atualização for concluída.  
  
 **Migração:** migrar uma versão anterior de uma instalação no modo nativo para o SQL Server Reporting Services exige as mesmas etapas para todas as versões compatíveis listadas anteriormente neste tópico. Para obter mais informações, veja [Migrar uma instalação do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
  
##  <a name="upgrade-a-reporting-services-native-mode-scale-out-deployment"></a><a name="bkmk_native_scaleout"></a> Atualizar uma implantação em expansão dos Reporting Services em modo nativo  
 Veja a seguir um resumo de como atualizar uma implantação de modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é dimensionada para mais de um servidor de relatório. Esse processo requer o tempo de inatividade da implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
1.  Faça backup dos bancos de dados do servidor de relatório e das chaves de criptografia. Para obter mais informações, consulte [Operações de backup e restauração do Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) e [Adicionar e remover chaves de criptografia para implantação escalável &#40; 	Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).  
  
2.  Use o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e remova todos os servidores de relatório da implantação em expansão. Para obter mais informações, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
3.  Atualize um dos servidores de relatório para o SQL Server Reporting Services.  
  
4.  Use o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para adicionar os servidores de relatório de volta para a implantação em expansão. Para obter mais informações, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
     Para cada servidor, repita as etapas de atualização e expansão.  
  
##  <a name="sharepoint-mode-upgrade-and-migration-scenarios"></a><a name="bkmk_sharePoint_scenarios"></a> Atualização do modo do SharePoint e cenários de migração  
 As seções a seguir descrevem os problemas e as etapas básicas necessárias para atualizar ou migrar de versões especificadas do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o modo do SharePoint do SQL Server Reporting Services [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Há dois componentes de instalação para atualizar uma implantação do modo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.  
  
    > [!TIP]  
    >  Use o cmdlet [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do `Get-SPRSServiceApplicationServers` SharePoint para determinar os servidores no farm do SharePoint que estão executando o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint e, portanto, requerem uma atualização.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Suplemento para produtos do SharePoint. Para obter mais informações, veja [Instalar ou desinstalar o Suplemento do Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Para obter etapas detalhadas sobre como migrar uma instalação no modo do SharePoint, consulte [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
> [!IMPORTANT]  
>  Alguns dos cenários a seguir exigem tempo de inatividade do ambiente do SharePoint devido às tecnologias diferentes que precisam ser atualizadas. Se a sua situação não permitir tempo de inatividade, você precisará concluir uma migração em vez de uma atualização in-loco.  
  
### <a name="sssql14-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para o SQL Server Reporting Services  
 **Ambiente inicial:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1, SharePoint 2010 ou SharePoint 2013.  
  
 **Ambiente final:** SQL Server Reporting Services, SharePoint 2013 ou SharePoint 2016.   
  
-   **SharePoint 2013/2016:** O SharePoint 2013/2016 não dá suporte à atualização in-loco do SharePoint 2010. No entanto, há suporte para o procedimento de **atualização da anexação do banco de dados**  .
  
     Se você tiver uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco. No entanto, você pode migrar bancos de dados de conteúdo e bancos de dados de aplicativo de serviço do farm do SharePoint 2010 para um farm do SharePoint 2013/2016.  
  
### <a name="sssql11-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para o SQL Server Reporting Services  
 **Ambiente inicial:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)], SharePoint 2010.  
  
 **Ambiente final:** SQL Server Reporting Services, SharePoint 2013 ou SharePoint 2016.   
  
-   **SharePoint 2013/2016:** O SharePoint 2013/2016 não dá suporte à atualização in-loco do SharePoint 2010. No entanto, há suporte para o procedimento de **atualização da anexação do banco de dados**  .
  
     Se você tiver uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco. No entanto, você pode migrar bancos de dados de conteúdo e bancos de dados de aplicativo de serviço do farm do SharePoint 2010 para um farm do SharePoint 2013/2016.  
  
### <a name="sskilimanjaro-to-sql-server-reporting-services"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para o SQL Server Reporting Services  
 **Ambiente inicial:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], SharePoint 2010.  
  
 **Ambiente final:** SQL Server Reporting Services, SharePoint 2013 ou SharePoint 2016.  
 
-   **SharePoint 2013/2016:** O SharePoint 2013/2016 não dá suporte à atualização in-loco do SharePoint 2010. No entanto, há suporte para o procedimento de **atualização da anexação do banco de dados**  .

    O SharePoint deve ser migrado primeiro antes da atualização do Reporting Services.
  
-   Instale a versão do SQL Server Reporting Services do suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint em cada front-end da Web no farm. Você pode instalar o suplemento usando o assistente de instalação do SQL Server Reporting Services ou baixando o suplemento.  
  
-   Execute a instalação do SQL Server Reporting Services para atualizar do modo do SharePoint em cada ‘servidor de relatório’. O assistente de instalação do SQL Server instalará o Serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e criará um novo aplicativo de Serviço. 
  
  
##  <a name="considerations-for-a-migration"></a><a name="bkmk_migration_considerations"></a> Considerações para uma migração  
 Ao mover dados de aplicativo, você deve estar atento às seguintes preocupações e restrições:  
  
-   A proteção da chave de criptografia inclui um hash que incorpora a identidade da máquina.  
  
-   Os nomes de banco de dados de servidor de relatório são fixos e não podem ser alterados em um novo computador.  
  
### <a name="encryption-key-considerations"></a>Considerações sobre a chave de criptografia  
 Sempre faça backup das chaves de criptografia antes de mover um banco de dados de servidor de relatório para um novo computador.  
  
 A migração de uma instalação do servidor de relatório para outro computador invalidará o hash que protege as chaves de criptografia usadas para ajudar a proteger dados confidenciais armazenados no banco de dados do servidor de relatório. Cada instância do servidor de relatório que usa o banco de dados tem sua cópia da chave de criptografia, que é criptografada com a identidade da conta de serviço, conforme definida no computador atual. Se você mudar de computador, o serviço não terá mais acesso à sua chave, mesmo que o mesmo nome de conta seja usado no novo computador.  
  
 Para restabelecer a criptografia reversível no novo computador do servidor de relatório, restaure a chave da qual fez backup anteriormente. O conjunto de chave completo que é armazenado no banco de dados do servidor de relatório consiste em um valor de chave simétrica e em informações sobre a identidade de serviço usada para restringir o acesso à chave, para que ela possa ser usada somente pela instância do servidor de relatório em que foi armazenada. Durante a restauração da chave, o servidor de relatório substitui as cópias existentes da chave pelas novas versões. A nova versão inclui os valores de identidade da máquina e de serviço, conforme definido no computador atual. Para obter mais informações, consulte estes tópicos:  
  
-   Modo SharePoint: confira a seção “Gerenciamento de chaves” em [Gerenciar um aplicativo de serviço do Reporting Services do SharePoint](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
-   Modo nativo: confira [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
### <a name="fixed-database-name"></a>Nome fixo do banco de dados  
 Você não pode renomear o banco de dados de servidor de relatório. A identidade do banco de dados é registrada em procedimentos armazenados do servidor de relatório quando o banco de dados é criado. A renomeação dos bancos de dados primário ou temporário do servidor de relatório provoca erros que ocorrem quando os procedimentos são executados, invalidando a instalação do servidor de relatório.  
  
 Se o nome do banco de dados da instalação existente não for adequado para a nova instalação, avalie a possibilidade de criar um novo banco de dados com o nome desejado e, em seguida, carregue os dados de aplicativo existentes usando as técnicas descritas na seguinte lista:  
  
-   Grave um script do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que chame métodos SOAP do serviço Web Servidor de Relatórios para copiar dados entre bancos de dados. Use o utilitário RS.exe para executar o script. Para obter mais informações sobre essa abordagem, veja [Script e PowerShell com o Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Grave o código que chama o provedor WMI para copiar dados entre bancos de dados. Para obter mais informações sobre essa abordagem, veja [Acessar o provedor WMI do Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
-   Se houver poucos itens, você poderá republicar relatórios e fontes de dados compartilhadas do Designer de Relatórios, do Designer de Modelo e do Construtor de Relatórios no novo servidor de relatório. Você deve recriar atribuições de função, assinaturas, agendas compartilhadas, agendas de instantâneo de relatório, propriedades personalizadas definidas em relatórios ou outros itens, segurança de item de modelo e propriedades definidas no servidor de relatório. Você perderá os dados do histórico de relatório e do log de execução de relatório.  
  
  
##  <a name="additional-resources"></a><a name="bkmk_additional_resources"></a> Recursos adicionais  
  
> [!NOTE]  
>  Para obter mais informações sobre a atualização da anexação do banco de dados do SharePoint, consulte o seguinte:  
  
-   [Visão geral do processo de atualização para o SharePoint 2016](https://technet.microsoft.com/library/cc262483\(v=office.16\)).

-   [Visão geral do processo de atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).
  
-   [Limpar preparações antes de uma atualização do SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Atualizar bancos de dados do SharePoint 2013 para o SharePoint 2016](https://technet.microsoft.com/library/cc303436\(v=office.16\)).

-   [Atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).  

## <a name="next-steps"></a>Próximas etapas

[Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md)   
[Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
